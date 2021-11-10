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
* **find empty **- flag used to include two additional buttons to the quick filter panel: a "Find empty" and "Find not empty" values. These buttons have their own CSS class: "filterempty" and "filternotempty". Use it only with a relational database. When flagging this check-box, you have also to change the x-theme.css content and define how to render these two buttons, according to your theme. If your them does not show icons but it shows text, you could change the grid filter section of your theme in this way:

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

Optionally, a group of** locked columns** can be anchored to the left side of the grid. In order to do it, set the "**Locked columns nr**" in the grid definition window.

In case **locked columns are combined with grouping columns, a new grid is rendered, composed of a tree+grid,** where grouping columns become tree nodes, which are anchored on the left side of the grid. That means it is not supported a grid having grouped columns+locked columns.
