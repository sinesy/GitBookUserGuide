# Multi Value Tree Filter

The multi value tree filter is a control available in the filter and editable panels. This control can filter the associated grid for one column with multiple values.

If the control is used in a filter panel the grid it refers is the same as specified for the panel.

In an editable panel you can apply the filter through a javascript action where you can get and use the selected data in the control.\
The selection of the values is carried out through a tree panel.

#### Configuration

You can configure the control in the Input Controls folder, by selecting the type "**Multi Value Tree**" and associating to the "Selector" property a selector having type "**Selector from panel**".

Before that, you have to configure a selector having type "Selector from panel":

![](<../../../.gitbook/assets/image (15).png>)

For this selector, you can specify the **tpl** for the selected item; if not specified, the default behavior is showing in the chip the code + description for the node.

![](<../../../.gitbook/assets/image (10) (1).png>)

If you want to show only the description or any other combination of attributes, you have top use "tpl" property.

In the web application, the end user can open the tree panel through the button on the right of control and then check multiple nodes on the tree.

The control shows a chip for every selected node.

![](<../../../.gitbook/assets/image (11) (1).png>)

To apply the filter on the grid you need to use the "**before search**" event to include the filter condition, since the filtering logic for a tree where you can check very different nodes is too complex to be automated. You can access to the selected codes (i.e. the list of unique identifiers for each selected node), through the combo method **getValue()**;

Example:

```
var treeCombo = findOwnerCtByItemId(win, 'filterPanel89').getComponent('controlMULTI_VALUE_TREE');
var values = treeCombo.getValue();
if(values != null && values != '') {
    filterNames += 'codArticolo,';
    filterOps += 'IN,';
    filterCaseSensitives += 'false,';
    filterValues += values + ',';
}
```

If you want to get all properties of a selected node (the embedded js object for a node), you can access it using the **currentFilters** combo property, which is an Array containing as many objects as the number of checked nodes (chips).&#x20;

Example:

```
var treeCombo = findOwnerCtByItemId(win, 'filterPanel89').getComponent('controlMULTI_VALUE_TREE');
var currentFilters = treeCombo.currentFilters;
for(var i=0; i<currentFilters.lenght; i++) {
    console.log(currentFilters[i]['properties']);
}
```
