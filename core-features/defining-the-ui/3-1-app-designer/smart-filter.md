# Smart Filter and Advanced Filter

## Smart Filter

The smart filter is a control available in the filter and editable panels. This control can filter the associated grid for multiple columns and multiple values.

If the control is used in a filter panel the grid it refers is the same as specified for the panel.

In an editable panel you have to specify the grid to link. For an editable panel, you can specify this grid with the control property [Additional Config](3-1-8-panels-list/3-1-8-4-controls-properties.md).\


#### Configuration

You can configure the control in the Input Controls folder (Smart Filter type) and associate an image selector to the smart filter.&#x20;

Note that the Operator property is useless, since the filters to apply to the grid use always the contains operator, since **it can be used only of text type fields**. If you need to filter on date/numeric fields, it is likely that the operator can change according to the need: for this scenario, it is better to use the advanced filter.

![](<../../../.gitbook/assets/image (4) (1) (1).png>)

The **image selector** is used to define the fields on which it is possible to search and the optional icon.

![](<../../../.gitbook/assets/image (5) (1) (1).png>)

If you don't want to use a selector image, you can specify a **javascript business component**, where you are free to define the fields to search. A business component is helpful in case you want to customize the behavior of the combobox and return a dynamic content, according to the text typed. However, it is not recommended to "pre-search" data in this business component, because the user experience can degrade because of the wait time for the additional queries.

The component id must be specified through the Additional config property, using the "compId" attribute.

![](<../../../.gitbook/assets/image (3) (1) (1).png>)

Optionally, it is also possible to customize the dropdown items content through the **tpl** property you can specify in the Additional Config settings. For example, the default value for the tpl property, if not specified, is as follows:

```
<div class='x-combo-list-item smart-filter-list-item'><img src='../{img}' /><span> {[this.translate(values.type)]} {value}...</span></div>
```



The business component must return a ListResponse object with the attributes required by the smart filter, whose names are reported in the following example:

```
var list = [];
list.push(
    {
        value: reqParams.value,
        type: utils.getResource('article'), // description for the field
        attributeName: 'articleField', //attribute name of field to search
        img: '/images/article.png', //icon for element
        operator: 'like'
    }
);
list.push(
    {
        value: reqParams.value,
        type: utils.getResource('barcode'), // description for the field
        attributeName: 'barcodeField', //attribute name of field to search
        img: '/images/barcode.png', //icon for element
        operator: '='
    }
);

utils.setReturnValue(utils.getListResponse(list, list.length, false));
```

Optionally, it is also possibile to customize how many characters to type in the smart filter before the dropdown list is shown: if not specified, it is set to 2 characters. You can override this default value by setting it in the Additional Config property of the smart filter:

```
minChars: 1,
```



**Behavior**

When the end user is typing a text, after a while, the dropdown list is shown, containing the content of the image selector (or the content of the business component).

Once the user selects one of the items from the dropdown list (i.e. a field) the smart filter content is changed to: "field: text" and the linked grid is automatically reloaded with an additional filter:

&#x20;"attribute" like '%text%'

At this point the user can press X to clear up the whole content of the smart filter (and the grid is reloaded again) or he can type a second text to search, separated by the already existing by a ;

The end user has to type ; text

Again, the smart filter shows the dropdown list and the end user has to choose a field. Once done that, the smart filter content is changed to: "field: text; secondfield: secondtext" and the linked grid is automatically reloaded with two additional filters:

&#x20;attribute like '%text%' AND  attribute2 like '%secondtext%'&#x20;

If you use the business component, for the smart filter control, you can specify the operator of condition for any attribute (like, <, >, =, >=, <=).

It is possible to customize the CSS classes for this widget, by overriding the corresponding CSS names in the app.css file.

## Advanced Filter

The Advanced Filter is available starting from the Smart Filter: when the Smart Filter is linked to a Filter Panel (which is NOT directly part of the window containing the Smart Filter), an additional button is shown on the right of the Smart Filter. This button is a switcher: when clicking on it, the Advanced Filter is shown, when clicking on it again, the Advanced Filter is hidden. When clicking again, the same Advanced Filter is shown again.

![](../../../.gitbook/assets/schermata-2021-06-24-alle-09.35.25.png)

To sum up, in order to have an Advanced filter, it is needed to:

*   create an Editor Panel or a Filter Panel, containing the Smart Filter; such a panel is part of the window containing the grid and the Smart Filter works on such a grid

    If you use a Editor Panel you must set the advanced filter to grid

```
gridXXX.advancedFilterPanel = filterPanelYYY;
```

* create a second Filter Panel (the Advanced Filter), by clicking on the grid and select Add Filter; do not add this second panel to the window
* fill in the Referred Panel property in the first panel, related to the Smart Filter Panel; fill it in with the second Filter Panel: in this way, the switcher icon on the Smart Filter will be rendered and used to open the Advanced Filter

It is possible to customize the CSS classes for this widget, by overriding the corresponding CSS names in the app.css file.







