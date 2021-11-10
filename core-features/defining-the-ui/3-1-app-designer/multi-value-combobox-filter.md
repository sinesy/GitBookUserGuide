# Multi Value Combobox Filter

The multi value combobox filter is a control available in the filter and editable panels. This control can filter the associated grid for one column with multiple values.

If the control is used within a filter panel the grid it refers is the same as specified for the panel.

In an editable panel you can apply the filter manually, through a javascript action, where you can get and use the data selected in the control.

#### Configuration

You can configure the control in the Input Controls folder, where you have to choose the type "**Dynamic Combobox**" and associate a selector; the selector must be a **dynamic selector** having the **Multi Value **checkbox selected (see image below).

![](<../../../.gitbook/assets/image (14).png>)

When the user types into the multi-value combobox, the typed value is validated and only matching values are shown.

![](<../../../.gitbook/assets/image (16).png>)

You can select an item and the control shows the relative chip. After that, you can type again another text and validation is performed again, in order to add additional items.

You can remove a chip by clicking on the X within it or remove all chips by clicking on the X on the right of the combobox.

![](<../../../.gitbook/assets/image (17).png>)

When you click on the search button, an IN type filter condition is applied to the grid with the selected values.
