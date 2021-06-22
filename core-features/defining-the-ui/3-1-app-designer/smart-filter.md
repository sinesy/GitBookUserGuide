# Smart Filter

The smart filter is a control available in the filter and editable panels. This control can filter the associated grid for multiple columns and multiple values.

If the control is used in a filter panel the grid it refers is the same as specified for the panel.

In an editable panel you have to specify the grid to link. For an editable panel, you can specify this grid with the control property [Additional Config](3-1-8-panels-list/3-1-8-4-controls-properties.md).  


#### Configuration

You can configure the control in the Input Controls folder \(Smart Filter type\) and associate an image selector to the smart filter. 

Note that the Operator property is useless, since the filters to apply to the grid use always the contains operator, since **it can be used only of text type fields**. If you need to filter on date/numeric fields, it is likely that the operator can change according to the need: for this scenario, it is better to use the advanced filter.

![](../../../.gitbook/assets/image%20%284%29.png)

The **image selector** is used to define the fields on which it is possible to search and the optional icon.

![](../../../.gitbook/assets/image%20%285%29.png)

If you don't want to use a selector image, you can specify a **javascript business component**, where you are free to define the fields to search. A business component is helpful in case you want to customize the behavior of the combobox and return a dynamic content, according to the text typed. However, it is not recommended to "pre-search" data in this business component, because the user experience can degrade because of the wait time for the additional queries.

The component id must be specified through the Additiona config property, using the "compId" attribute.

![](../../../.gitbook/assets/image%20%283%29.png)

The business component must return a ListResponse object with the attributes required by the smart filter, whose names are reported in the following example:

```text
var list = [];
list.push(
    {
        value: reqParams.value,
        type: utils.getResource('article'), // description for the field
        attributeName: 'articleField', //attribute name of field to search
        img: '/images/article.png' //icon for element
    }
);
list.push(
    {
        value: reqParams.value,
        type: utils.getResource('barcode'), // description for the field
        attributeName: 'barcodeField', //attribute name of field to search
        img: '/images/barcode.png' //icon for element
    }
);

utils.setReturnValue(utils.getListResponse(list, list.length, false));
```



**Behavior**

When the end user is typing a text, after a while, the dropdown list is shown, containing the content of the image selector \(or the content of the business component\).

Once the user selects one of the items from the dropdown list \(i.e. a field\) the smart filter content is changed to: "field: text" and the linked grid is automatically reloaded with an additional filter:

 "attribute" like '%text%'

At this point the user can press X to clear up the whole content of the smart filter \(and the grid is reloaded again\) or he can type a second text to search, separated by the already existing by a ;

The end user has to type ; text

Again, the smart filter shows the dropdown list and the end user has to choose a field. Once done that, the smart filter content is changed to: "field: text; secondfield: secondtext" and the linked grid is automatically reloaded with two additional filters:

 attribute like '%text%' AND  attribute2 like '%secondtext%' 



