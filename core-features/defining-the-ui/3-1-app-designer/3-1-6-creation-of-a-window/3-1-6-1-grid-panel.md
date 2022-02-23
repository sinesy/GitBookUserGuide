# Grid Panel

**In case of grid or filter+grid or grid+detail form** , the grid definition panel is showed; through it the user has to define settings related to the grid component:

* **grid** **title** (optional, can be hidden)
* **business component** (for list of data) to link to the grid; the fields specified in the select clause are used to automatically&#x20;
* create the grid columns; user can then **show/hide** each of them, as well as define many other column settings
* grid **width** and **height**
* flags to **show/hide border** and to set panel opacity
* flags to **allow the CRUD operations**, i.e. insert, update and delete (only if the data model linked to the selected business component is writable); in case of insert enabled, it is possible to specify the maximum number of rows to insert before saving them
* **data fetching policy**: read all or a block of data and its size
* flag to define if **data loading is automatically performed** when the grid is showed
* **initial grid mode**, when the grid is showed; grids and forms have 3 alternative modes: readonly, insert, edit; in insert mode a new row is showed; through up/down arrows is possible to add/remove (empty) rows; in edit mode, all rows are editable or the one only (selected row), according to the flag "multiple changes"
* flag "**copy enabled**", used to show a "copy" button in the grid toolbar, used to switch to insert mode the grid, add a new row an copy the values from the selected row to the new one
* number of **columns anchored to the lef**t of the grid (0 by default)
* boolean javascript expression "**disable when**", to disable everything when the boolean condition is true flags "enable columns permission" and "enable columns profile", used to manage these special features, described in a separate section
* **find empty** - flag used to include two additional buttons to the quick filter panel: a "Find empty" and "Find not empty" values. These buttons have their own CSS class: "filterempty" and "filternotempty". Use it only with a relational database. When flagging this check-box, you have also to change the x-theme.css content and define how to render these two buttons, according to your theme. If your them does not show icons but it shows text, you could change the grid filter section of your theme in this way:

```javascript
/* filtro in griglia*/

    .x-panel.w-filter{
        background-color: var(--panel-light-background);
    }
    .w-filter .x-panel,
    .w-filter .x-panel-header,
    .w-filter .x-panel-body{
        background-color: transparent;
    }

    #filterMenu .x-plain-header{
        padding-top: 5px
    }
    #filterMenu .x-plain-header-text b{
        font: 10pt arial;
        margin-left: 7px;
    }
    #filterMenu .x-panel.x-panel-noborder.x-abs-layout-item{
        margin-top: 5px;
    }
    .x-filter-panel .x-btn-text-icon .x-btn-icon-small-left .x-btn-text,
    #filterMenu .x-btn-text{
        margin: 0px 7px;
    }
    /* tasto filtra in griglia */
    div#filterMenu table:first-of-type{
    	top: 65px !important;
        left: 0px !important;
    }
    /* tasto rimuovi filtra in griglia */
    div#filterMenu table:last-of-type{
    	top: 65px !important;
        left: 125px !important;
    }
    #filterMenu .x-btn-text.filter,
    #filterMenu .x-btn-text.filterempty,     /* <-- NEW ENTRY */
    #filterMenu .x-btn-text.filternotempty,  /* <-- NEW ENTRY */
    #filterMenu .x-btn-text.removefilter{
		width: 100px;
		text-indent:0;
		border-radius: 5px;
		padding: 0;
	}


	#filterMenu .x-btn-text.filter,
	#filterMenu .x-btn-text.filterempty,      /* <-- NEW ENTRY */
	#filterMenu .x-btn-text.filternotempty{   /* <-- NEW ENTRY */
		border: 2px solid #44ceb0;
		color: #44ceb0;
    }
	#filterMenu .x-btn-text.removefilter{
		border:2px solid #F2627D;
		color: #F2627D;
	}

	#filterMenu .x-btn-text.filter:hover,
	#filterMenu .x-btn-text.filterempty:hover,      /* <-- NEW ENTRY */
	#filterMenu .x-btn-text.filternotempty:hover{   /* <-- NEW ENTRY */ 
		background-color: #bdf9ec;
	}
	#filterMenu .x-btn-text.removefilter:hover{
		background-color: #F0CBD2;
	}
	#filterMenu .x-form-text{
		height: 20px;
	}

	#filterMenu .x-form-field-wrap.x-form-field-trigger-wrap.x-trigger-wrap-focus{
		width: 224px !important;
	}

	#filterMenu .x-form-trigger.x-form-arrow-trigger{
		background-position-y: 0;
		background-color: transparent;
	}

    .x-filter-panel, .x-filter-panel .x-plain-header, .x-filter-panel .x-plain-body, .x-window .x-filter-panel form.x-plain-body{
        background: var(--panel-light-background);
    }
    .x-filter-panel{
    	padding-left:10px;
    }
    .x-filter-panel input{
    	background: white;
    }
    .x-tool-toggle{
    	background-position: center;
    	border-radius: 8px;
    }
```

When creating the grid, a grid toolbar is automatically showed on top of it; this toolbar always includes the reload button; the other buttons (insert, edit, delete and save/cancel) are showed/hidden according to the flags described above.\
These buttons change the current grid mode, according to the following policy:

* insert button, from readonly mode -> insert mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* edit button, from readonly mode -> edit mode, insert/edit/delete buttons are disabled, save/cancel buttons are enabled
* delete button, from readonly mode -> after confirming the operation, the selected records are deleted
* cancel button, from insert/edit mode -> after confirming the operation, the grid is switched to readonly mode and the content reloaded
* save button, from insert/edit mode -> the grid is switched to readonly mode if the saving operation has been performed successfully.

## Column types

Through the "**type**" property for a column, it is possible to set a wide range of different columns; they differ for the way they are rendered, according to the current cell mode: rendering or editing (i.e. when the user clicks on it and an editor is showed).

Supported types are:

* **Button** - a clickable button is rendered in both modes; a click event can be linked to it, through Column Events folders
* **CMS File** - it shows a clickable button to use when the grid is used combined with the "Internal CMS module"; the button leads to a File Upload Dialog, to manage File upload/download/Preview and its automatic reading/writing into the CMS module; when this type is set, the **Directory** property must be set as well
* **Checkbox** - a checkbox is rendered in both modes and the checkbox is clickable in insert/edit grid modes; when this type is set, also Positive/Negative value properties must be set
* **Counter based on a component** - this type cannot be changed, since it is inherited by the bounded data model
* **Counter based on a table** - this type cannot be changed, since it is inherited by the bounded data model
* **Date** - it shows a date formatted according to the current user language; in insert/edit grid mode, the cell is editable and a calendar can be opened to choose the date
* **Date+Time** - it shows a date+time formatted according to the current user language; in insert/edit grid mode, the cell is editable and a calendar can be opened to choose the date
* **Dynamic Combobox** - when rendered, a text is showed; the text corresponds to the current code set in the cell; in insert/edit grid mode, a combobox is showed as editor and the user can type a few characters to limit the items list or click on the trigger button to  open the dropdown list, which is always paginated; data is retrieved through the server, where a business component is invoked: data is dynamic; when filling this type, the **Selector** property must be set too. See [https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors](https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors) for more details.
* **File Id** - it shows a clickable button to use when the grid is used combined with the "Alfresco ECM module"; the button leads to a File Upload Dialog, to manage File upload/download/Preview and its automatic reading/writing into the Alfresco module; when this type is set, the **Directory** property must be set as well&#x20;
* **File Path** - it shows a file name or a button (in insert/edit grid mode) to choose a file; when filling this type, the **Directory** property must be set too
* **Image URL -** it shows an image as a preview; the cell contains behind the scenes the image file name; cell editing is not allowed; when filling this type, the **Directory** property must be set too
* **Images Combobox -** when rendered, an image is showed; the image corresponds to the current file name set in the cell; in insert/edit grid mode, a combobox is showed as editor and the user choose among a list of images rendered as combo items; when filling this type, the **Selector** property must be set too. See [https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors](https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors) for more details.
* **Internal counter** - this type cannot be changed, since it is inherited by the bounded data model
* **Lookup Button** - there is no rendering value for this type; when editing the cell, a "lookup button" is rendered and used to open a "lookup grid", in order to select a code from the list. See [https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors](https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors) for more details.
* **Lookup Cod/Button** - the cell value is showed when rendering the cell; when editing the cell, an "input text field" + "lookup button" are rendered; when losing focus from the cell, the typed text is validated; when clicking on the button a "lookup grid" is showed, in order to select a code from the list. See [https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors](https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors) for more details.
* **Number -** numeric input field, with a large variety of different properties; support for integer/decimal/currency values
* **Path images** - ?
* **Sequence/Autoincrement -** this type cannot be changed, since it is inherited by the bounded data model
* **Static Combobox -** when rendered, a text is showed; the text corresponds to the current code set in the cell; in insert/edit grid mode, a combobox is showed as editor and the user can type a few characters to limit the items list or click on the trigger button to  open the dropdown list, which contains a static predefine list of items (code+description, where description is translated according to the current user language); when filling this type, the **Selector** property must be set too. See [https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors](https://4wsplatform.gitbook.io/user-guide/core-features/defining-the-ui/3-1-app-designer/3-1-10-code-selectors) for more details.
* **Text** - text input field
* **Text area** - multi-line text field (not a very good choice for a grid...)
* **Time only** - it shows a date formatted according to the current user language; in insert/edit grid mode, the cell is editable and a calendar can be opened to choose the date
* **Tree Lookup -** no value is showed when rendering the cell; when editing the cell, a "lookup button" is rendered: when clicking on the button a "lookup tree" is showed, in order to select a node from the list (the code to set in the cell); when filling this type, the **Selector** property must be set too
* **UUID** **-** this type cannot be changed, since it is inherited by the bounded data model
* **Upload to directory** - an old version type; it is recommended not to use it any more



## Summary row

Optionally, a **summary locked row** can be showed on the bottom of the grid; this read only row is automatically showed only if there is an "update summary row" event linked to the grid: in that case it will be showed and the javascript action binded to the event is invoked for each column, every time a cell is changed.\
In order to avoid setting a total value for a specific cell, a ‘’ can be returned to that callback in the action. It is possible to set foreground and background colors for a cell through css class names (see details specified below for the "update summary row" event).

Example:

```javascript
if (colAttr!='attributenameofaspecificcolumn') return '';
return formattedValue;
```

or

```javascript
params.css = 'red';
return total;
```

## Grouped columns in multiple groups

Optionally , it is possible to **group columns in multiple groups**, so that there will be a hierarchy of headers, spread in multiple header rows.

In order to do it, add the "Column header" panel event to the grid and define a client-side javascript action containing the headers definition.

**Important note:** pay attention to the hidden columns. With grouped columns you have not to make "selectable" any other non visibile column and it would be better to make them "not managed as well". As an alternative, you have to move all visible columns at the beginning and move all not selectable, not visibile but managed columns all on the right.

An example of such a definition is the following:

```javascript
// example for 45  columns, grouped in 5 main headers
// colspan is used to define how many headers to include in each main header
return [[
{ // first main header
    header: ' ',
    colspan: 10
}, { // second main header 
    header: Ext.translate.Cache.getTranslation('SECOND_TITLE'),
    align: 'center',
    colspan: 3
}, {
    header: Ext.translate.Cache.getTranslation('THIRD_TITLE'),
    align: 'center',
    colspan: 3
}, {
    header: Ext.translate.Cache.getTranslation('FORTH_TITLE'),
    align: 'center',
    colspan: 4
}, {
    header: Ext.translate.Cache.getTranslation('FIFTH_TITLE'),
    align: 'center',
    colspan: 25
}
]];
```

## Locked columns

Optionally, a group of **locked columns** can be anchored to the left side of the grid. In order to do it, set the "**Locked columns nr**" in the grid definition window.

In case **locked columns are combined with grouping columns, a new grid is rendered, composed of a tree+grid,** where grouping columns become tree nodes, which are anchored on the left side of the grid. That means it is not supported a grid having grouped columns+locked columns.
