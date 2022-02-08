# Form Panel

**In case of detail form or grid+detail form** , the form definition panel is showed; through it the user has to define settings related to the form component:

* form title (optional, can be hidden)
* business component (for a single record loading) to link to the form; the fields specified in the select clause are used to automatically create the form controls; user can then show/hide each of them, as well as define many other control settings
* form width and height
* flags to show/hide border and to set panel opacity
* flags to allow the CRUD operations, i.e. insert, update and delete (only if the data model linked to the selected business component is writable);
* flags to define if the window embedding the detail form must be closed after the operations of insert/update/delete
* flag to define if data loading is automatically performed when the form is showed
* initial form mode, when the form is showed; grids and forms have 3 alternative modes: readonly, insert, edit; in insert mode all controls are cleared up
* flag "copy enabled", used to show a "copy" button in the form toolbar, used to switch to insert mode the form, clear up all controls and then copy the values from the previous record to the new one
* boolean javascript expression "disable when", to disable everything when the boolean condition is true
* linked grid, used to manage some default operations, such as the grid reloading after inserting/updating the form content
* number of columns and label length, used to define the labels+controls layout; it is also possible to arrange labels and controls by specifying the x and y coordinates for each of them.
*   flags "enable tag" and "enable rating" used only for detail form based on a business component that uses Alfresco service.

    **Important note:** when defining a form panel, a linked grid should be selected; in this way, Platform can automate many operations involved with the interaction between grid and form: automatic form opening when double clicking on a grid, form loading when selecting a row in grid, grid content automatic update when saving/deleting data in the form.\
    However, **it is also allowed not to set any linked grid when defining the form** : in that case, the form is disconnected from any other panel and the previous automatisms are not available; that means that the required input parameters for the form must be explicitelly provided by the programmer, for example when opening a window containing that form. This is relatively easy to do, by passing to the openWindowXXX(args) instruction the required input parameters through the args obiect.\
    If case the form (not linked to any grid) is **directly opened starting from a menu item** , there aren’t any input values passed to the window containg the form; it that case, the required input parameters must be defined within the window and before the creation of the form. That means that t **he required input parameters must be defined through a javascript action linked to the "before render" event of the window** , which can be defined in the window detail form.

When creating the form, a form toolbar is automatically showed on top of it; this toolbar always includes the reload button; the other buttons (insert, edit, delete and save/cancel) are showed/hidden according to the flags described above.\
These buttons change the current form mode, according to the following policy:

* insert button, from readonly mode -> insert mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* edit button, from readonly mode -> edit mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* delete button, from readonly mode -> after confirming the operation, the selected records are deleted
* cancel button, from insert/edit mode -> after confirming the operation, the form is switched to readonly mode and the content reloaded
* save button, from insert/edit mode -> the form is switched to readonly mode if the saving operation has been performed successfully.





## Control types

Through the "**type**" property for a control, it is possible to set a wide range of different controls.

Every control is usually composed of:

* a label; it can be rendered either on the left or on top of the input field
* an input field; according to the type, the field can be read-only (a button, an image type control) or editable or can miss at all (e.g. a label type control).

Supported types are:

* **Button** - a clickable button; a click event can be linked to it, through Column Events folders
* **CMS File** - it shows a clickable button to use when the form panel is used combined with the "Internal CMS module"; the button leads to a File Upload Dialog, to manage File upload/download/Preview and its automatic reading/writing into the CMS module; when this type is set, the **Directory** property must be set as well
* **Checkbox** - the checkbox is clickable in insert/edit grid modes; when this type is set, also **Positive**/**Negative** **value** properties must be set
* **Counter based on a component** - this type cannot be changed, since it is inherited by the bounded data model
* **Counter based on a table** - this type cannot be changed, since it is inherited by the bounded data model
* **Date** - it shows a date formatted according to the current user language; in insert/edit mode a calendar can be opened to choose the date
* **Date+Time** - it shows a date+time formatted according to the current user language; in insert/edit mode, a calendar can be opened to choose the date
* **Dynamic Combobox** - a combobox where the user can type in a few characters to limit the items list or click on the trigger button to  open the dropdown list, which is always paginated; data is retrieved through the server, where a business component is invoked: data is dynamic; when filling this type, the **Selector** property must be set too
* **File Id** - it shows a clickable button to use when the form panel is used combined with the "Alfresco ECM module"; the button leads to a File Upload Dialog, to manage File upload/download/Preview and its automatic reading/writing into the Alfresco module; when this type is set, the **Directory** property must be set as well&#x20;
* **File Path** - it shows a file name (and a button in insert/edit mode) to choose a file; when filling this type, the **Directory** property must be set too
* **HTML** - a read only control composed of a HTML area when showing any kind of HTML scriptlet; helpful when very complex content must be showed within the form
* **HTML Editor** - an HTML editor to use to write formatted text (e.g. with bold, italics, fonts, etc)
* **Image URL -** it shows an image as a preview; the cell contains behind the scenes the image file name; this control cannot be "edited"; when filling this type, the **Directory** property must be set too
* **Images Combobox -**  a combobox rendering an image; when the user chooses among a list of images rendered as combo items, a new image is set/showed in the control; when filling this type, the **Selector** property must be set too
* **Internal counter** - this type cannot be changed, since it is inherited by the bounded data model
* **Label** - a component composed of a label only: no input field is showed
* **Lookup Button** - a "lookup button" is rendered and used to open a "lookup grid", in order to select a code from the list
* **Lookup Cod/Button** - an "input text field" + "lookup button" are rendered; when losing focus from the input text field, the typed text is validated; when clicking on the button a "lookup grid" is showed, in order to select a code from the list
* **Number -** numeric input field, with a large variety of different properties; support for integer/decimal/currency values
* **Password** - an input text field, where typed character are never showed in plain mode, but they are replaced by \*
* **Radio button** - a radio button is rendered; they are always used combined with other radio buttons
* **Sequence/Autoincrement -** this type cannot be changed, since it is inherited by the bounded data model
* **Static Combobox -** a combobox is showed and the user can type in a few characters to limit the items list or click on the trigger button to  open the dropdown list, which contains a static predefine list of items (code+description, where description is translated according to the current user language); when filling this type, the **Selector** property must be set too
* **Text** - text input field
* **Text area** - multi-line text field (not a very good choice for a grid...)
* **Time only** - it shows a date formatted according to the current user language; a calendar can be opened to choose the date part
* **Tree Lookup -** a "lookup button" is rendered: when clicking on the button a "lookup tree" is showed, in order to select a node from the list (the code to set in the cell); when filling this type, the **Selector** property must be set too
* **UUID** **-** this type cannot be changed, since it is inherited by the bounded data model
* **Upload to directory** - an old version type; it is recommended not to use it any more
