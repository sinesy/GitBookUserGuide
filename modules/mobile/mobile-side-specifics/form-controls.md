# Form Controls

The controls of a form can be of this type:

* Label
* Text \(normal text, email, password\)
* Multiline text
* Number
* Combobox
* Checkbox
* Date
* Date time
* Time
* Button Lockup
* Code/Description Button Lockup
* Image  \(url or path\)
* Address autocomplete

## Address autocomplete

This kind of field  use the Google Place API for suggest a valid address to the user. In order to use this control you need a GCP  project with a billing account and the Places API enabled, then:

1. In the Cloud Console, on the project selector page, select or create a Google Cloud project for which you want to add an API Key.
2. Go to the **APIs & Services &gt; Credentials** page.
3. On the Credentials page, click Create credentials &gt; API key.

   The API key created dialog displays your newly created API key.

4. It's  important to restrict your key by select  an app id, a keystore and by select Places SDK for Android and Place SDK
5. repeat steps 2-3-4 for iOs
6. Finally, in the Platform Application params go to Mobile folder and set the Autocomplete key for iOs and Android

This control has 2 **events**:

* **select**: fire when user click and address
* **change**: fire after select if user select  a different address from previous

In the change event you can use the method getFormPanelAddressValue for fill other fields \([se API Docs](https://4wsplatform.gitbook.io/api/mobile-javascript-api/forms#getformpaneladdressvalue-panelid-attr)\).

Note: setFormPanelValue not fire any events of this fields, and getFormPanelValue return only the route not the full address.



