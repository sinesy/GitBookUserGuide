# Smart Filter

The smart filter controls is a control for filter and form panels. This control can filter the associated grid for more fields and more values.  
If the control is used in a filter panel the grid it refers to is the same as specified for the panel, in form panel you can specify another grid. You can set this properties with [Additional Config](3-1-8-panels-list/3-1-8-4-controls-properties.md).  


#### Configuration

You can configure the control in the control panel and associate the filter field with a image selector

![](../../../.gitbook/assets/image%20%284%29.png)

The image selector is used to indicate the fields on which it is possible to search and the optional icon.

![](../../../.gitbook/assets/image%20%285%29.png)

If you don't want use a selector image you can specify the business component for the fields to search.

![](../../../.gitbook/assets/image%20%283%29.png)

The business component must return a ListResponse object with specify attribute. Example:

```text
var list = [];
list.push(
    {
        value: 'text to search',
        type: utils.getResource('article'), //text for control
        attributeName: 'articleField', //attribute name of field to search
        img: '/images/article.png' //icon for element
    }
);
list.push(
    {
        value: 'text to search',
        type: utils.getResource('barcode'), //text for control
        attributeName: 'barcodeField', //attribute name of field to search
        img: '/images/barcode.png' //icon for element
    }
);

utils.setReturnValue(utils.getListResponse(list, 2, false));
```

