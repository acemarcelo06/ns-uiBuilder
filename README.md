# UIBuilder Library - Usage Guide

This library helps you easily create custom UIs and sublists for **NetSuite** forms. Below is a comprehensive guide on how to use it.

## Table of Contents
1. [Add Field Tabs](#add-field-tabs)
2. [Add Field Group](#add-field-group)
3. [Add Fields to Mainline](#add-fields-to-mainline)
4. [Set Default Value for a Field](#set-default-value-for-a-field)
5. [Add Submit and Custom Buttons](#add-submit-and-custom-buttons)
6. [Set Form Title](#set-form-title)
7. [Add Sublist](#add-sublist)
8. [Set Sublist Values](#set-sublist-values)

---

## 1. Add Field Tabs

To create tabs in your form, use the following approach:

```javascript
// Define tabs
var tabs = [{
    id: 'tabs',
    label: 'Tabs'
}];

// Add tabs to the form
form = uibuilder.addTabs(tabs, form);
```

---

## 2. Add Field Group

To group fields, define the group and add it to the form:

```javascript
// Define field group
var grouping = [{
    id: 'filters',
    label: 'Filters'
}];

// Add group to the form
form = uibuilder.addGroups(grouping, form);
```

---

## 3. Add Fields to Mainline

Define the fields for the form's mainline and then add them:

```javascript
var fields = [{
    props: {
        id: 'custpage_07_subsidiary',
        type: ui.FieldType.SELECT,
        label: 'Subsidiary',
        source: 'subsidiary',
        container: 'filters'
    },
    value: null,
    options: null,
    isMandatory: true,
    updateBreakType: ui.FieldBreakType.STARTCOL,
    updateDisplayType: ui.FieldDisplayType.NORMAL,
}];

form = uibuilder.addFields(fields, form);
```

---

## 4. Set Default Value for a Field

To set a default value for a field:

```javascript
var subField = form.getField({
    id: 'custpage_07_subsidiary'
});
subField.defaultValue = subsidiary;
```

---

## 5. Add Submit and Custom Buttons

Add a **submit button** and a **custom button**:

```javascript
form.addSubmitButton({
    label: 'Submit',
});

form.addButton({
    id: 'custpage_07_backtomain',
    label: 'Back To Main',
    functionName: 'backToMain'
});
```

---

## 6. Set Form Title

To set the form's title:

```javascript
form.title = "Currently processing data...please wait.";
```

---

## 7. Add Sublist

To add a sublist to the form:

```javascript
fields.push({
    props: {
        id: 'custpage_07_account',
        type: ui.FieldType.TEXT,
        label: 'Account',
        source: null,
    },
    value: null,
    options: null,
    isMandatory: false,
    updateBreakType: ui.FieldBreakType.NONE,
    updateDisplayType: ui.FieldDisplayType.INLINE,
}, {
    props: {
        id: 'custpage_07_tenantid',
        type: ui.FieldType.TEXT,
        label: 'Tenant',
        source: null,
    },
    value: null,
    options: null,
    isMandatory: false,
    updateBreakType: ui.FieldBreakType.NONE,
    updateDisplayType: ui.FieldDisplayType.HIDDEN,
}, {
    props: {
        id: 'custpage_07_tenant',
        type: ui.FieldType.TEXT,
        label: 'Tenant',
        source: null,
    },
    value: null,
    options: null,
    isMandatory: false,
    updateBreakType: ui.FieldBreakType.NONE,
    updateDisplayType: ui.FieldDisplayType.INLINE,
});

sublists = [{
    'props': {
        'id': 'custpage_07_accountlist',
        'type': ui.SublistType.LIST,
        'label': 'Results(' + accountValues.length + ')',
    },
    'fields': fields,
}];

form = uibuilder.addSublists(sublists, form);
```

---

## 8. Set Sublist Values

To populate the sublist with values, follow this approach:

```javascript
// Note: {accountValues} is an array of objects with keys set to internal IDs of sublist fields
var sublistValues = [{
    sublistId: 'custpage_07_accountlist',
    values: accountValues
}];

form = uibuilder.populateSublists(sublistValues, form);
```

---

## Additional Notes:

- **Testing**: Always test the form in a sandbox environment before deploying to production.
- **Customization**: Feel free to modify and extend the library according to your project needs.
```