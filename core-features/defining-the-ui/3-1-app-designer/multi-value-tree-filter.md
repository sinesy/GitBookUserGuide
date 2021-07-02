# Multi Value Tree Filter

The multi value tree filter is a control available in the filter and editable panels. This control can filter the associated grid for one column and multiple values.

If the control is used in a filter panel the grid it refers is the same as specified for the panel.

In an editable panel you can apply the filter with a javascript action using the data selected in the control.  
The selection of the values is done through a tree panel.

#### Configuration

You can configure the control in the Input Controls folder \(Multi Value Tree\) and associate an "Selector from panel" with a tree panel linked.

![](../../../.gitbook/assets/image%20%2815%29.png)

For this selector you can specify the tpl for the selected item

![](../../../.gitbook/assets/image%20%2810%29.png)

The user can be open the tree panel with the button on the right of control and can select more values from tree.

The control contains a chip for any selected node.

![](../../../.gitbook/assets/image%20%2811%29.png)

To apply the filter on the grid you need to add the "before search" event to create the filter condition. Example:

```text
var values = findOwnerCtByItemId(win, 'filterPanel89').getComponent('controlMULTI_VALUE_TREE').getValue();
if(values != null && values != '') {
    filterNames += 'codArticolo,';
    filterOps += 'IN,';
    filterCaseSensitives += 'false,';
    filterValues += values + ',';
}
```

If you want view all properties of selected node you can read the current filter of control. Example:

```text
var currentFilters = findOwnerCtByItemId(win, 'filterPanel89').getComponent('controlMULTI_VALUE_TREE').currentFilters;
for(var i=0; i<currentFilters.lenght; i++) {
    console.log(currentFilters[i]['properties']);
}
```

