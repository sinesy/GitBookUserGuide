# Preview Panel \(old Image panel\)

You can use the Preview Panel to show different documents, **as long as their preview is supported by the browser** \(so that the .xls or .doc are not any more supported formats that a browser can render\).

The Preview Panel can be configured in a few alternative ways, described as follows. 

If you configuring the Preview Panel for a mobile app, please see the ad hoc section in the mobile chapter:

{% embed url="https://4wsplatform.gitbook.io/user-guide/modules/mobile/mobile-side-specifics/ee7-2-5-window-content/preview-panel" %}

You can set up a Preview Panel in these ways:

* **to show and edit an image/document** stored by Platform within a folder defined through a directory; in this case, there is a toolbar you can use not only to see the preview, but also to download it and change \(upload\) a new image. In such a scenario, you have to choose 
  * Preview Format: Document/Image Preview
  * Directory: the one used to save/retrieve images
  * Business component: a detail b.c. used to retrieve a record containing the file name related to the image/document to show
  * URI/resource to show: a field name related to the object linked to the selected business component which contains the file name
  * image width and height
  * flags to show/hide border and to set panel opacity
* **to show a read only remote document**, accessible through the web \(a public resource\); in this case, you have to fetch the URL to invoke, showed in an embedded iframe generated automatically by Platform. In such a scenario, you have to choose 
  * Preview Format: URL Preview
  * Business component: a detail b.c. used to retrieve a record containing the URL to use to get the web resource to preview
  * URI/resource to show: a field name related to the object linked to the selected business component which contains the URL
* **to show a read only web resource, starting from a custom HTML fragment**; in this case, you have to choose 
  * Preview Format: HTML Template
  * URI/resource to show: the HTML template to select; this HTML template should contain a static URL or a dynamic URL where part of it is parameterized as :XXX variables; these variables are replaced on the server side, starting from the internal state.

\*\*\*\*

### **Filling in the Preview content**

Optionally, it is possible to select the "**Autoload when opening**" checkbox: use it when the resource to show is "static", i.e. already reckoned starting from the preview itself or the internal state. 

A few examples where checking the "Autoload when opening" flag:

* an **image** must be showed and the **business component** has been defined: the business component must contain the file name to use to fill in the preview
* an **remote document** must be showed and the **business component** has been defined: the business component must contain the URL to use to fill in the preview
* a **template** is used to fill in the preview and the **HTML fragment is completely filled** either because it is static or the :XXX variables in it are already known on the server-side \(es. :COMPANY\_ID, :USERNAME, etc.\); consequently, do not check this flag if the specified variables are not known simply starting from the server-side user session.

An alternative approach to fill in a preview is using a client-side event linked to some panel already visible and use it to **programatically** fill the content.

In case of a **template** based preview, it depends on the HTML fragment you included. For example, in case of an HTML fragment like this:

```text
<iframe src=":MYURL"></iframe>
```

You can access the iframe tag through the classical **getComponentByItemId** method and then access to the src attribute:

```text
var sel = gridYYY.getSelectionModel().getSelected(); // the selected row in a grid, used to fetch data used to fill in the preview
if (sel!=null) {
  var imagePanel = getComponentByItemId("imagePanelXXX",win);
  var iframe = imagePanel.getEl().dom.children[0].children[0].children[0];
  iframe.src = sel.myAttributeContainingTheURL;
}
```



In case of a **remote document** based preview, you can use the loadImageXX utility method provided by Platform to access the preview panel and force its reloading, starting from a record coming from another panel:

```text
var sel = gridYYY.getSelectionModel().getSelected(); // the selected row in a grid, used to fetch data used to fill in the preview
if (sel!=null) {
  imagePanelXXX.removeAll();
  imagePanelXXX.doLayout();
  loadImagePanelXXX(sel.data);
}
```



