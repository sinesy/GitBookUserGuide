# Buttons

Buttons can be added to the toolbar included on the top of a grid or a detail form. In the detail window related to grids or forms, there is a special folder named "Buttons" that allows to insert, edit, delete custom buttons.\
For each of these buttons, an action can be called when the user presses the button.\
Apart from the action binded to the button, there are other properties that can be defined when creating a button:

* **text** for the button
* button **icon**
* **position** of the button inside the toolbar
* flag used to the way the action is invoked: either **synchronous** or **asynchronous**
* flag used to **enable** the button only when the component (grid/form) is in **insert** mode
* flag used to **enable** the button only when the component (grid/form) is in **edit** mode
* flag used to **enable** the button only when the component (grid/form) is in **readonly** mode
* **style** used to include CSS content for an web based Platform application (optional)
* flag used to **hide** the button when a **boolean javascript condition** is true (the condition can include :XXX variables as well)
* flag used to **disable** the button when a **boolean javascript condition** is true (the condition can include :XXX variables as well); this property will override the default behavior defined through the other 3 flags described above, working on a specific panel mode

Through buttons it is possible to open windows from parent windows, execute business logic on the server side, perform other presentation logic, through actions, expressed as javascript, SQL statements, web services.



### Link-type buttons, alignments and group of buttons

For **grid**, **form** and** buttons panels** the following additional properties are also available:&#x20;

* **Group style** - in case a button is part of a group of buttons (i.e. the "Group name" property has been filled), it is possible to specify how to group of buttons must be rendered, among 3 alternatives; all buttons belonging to the same group must have the same group style, which can be:
  * as a **combobox**, i.e. all buttons belonging to the same group are shown within a combo button (split button), with the first button of the group directly shown as the first choice and directly clickable without opening the combo (helpful to quick choices)
  * as a **single selection** group of buttons, i.e. all buttons are shown close to each other, with round boxes and only one can be clicked per time, since all buttons are toggle buttons; in such a scenario, it is also possible to use the "**Preset**" property to define the button in the group which must be pre-selected
  * as a **multiple selection** group of buttons, i.e. all buttons are shown close to each other, with round boxes and zero or more buttons can be clicked per time and all buttons are toggle buttons
* **Group name **- used to define a group name (no spaces or special characters are allowed for the group name); all buttons belonging to the same group must have the same group name and they must be defined in a consecutive order.
* **Alignment** - used to change the default horizontal alignment of a button: it is possibile to align the button to the right border of the panel; this feature is not available for a buttons panel, since its alignment is always horizontal centered.
* **Preset** - flag used in case of a group of panels having "Single selection" group style, to define the one only button in the group receiving a pre-selected state
* **Button style** - it defines how the button will be rendered: the default style is as a button; as an alternative, it is possible to render it as a link

### Examples and CSS customizations

#### Single selection buttons

Additional properties to set:

* Group name: the same for the 3 buttons
* Preset: checked for the first button
* Group style: Single selection for the 3 buttons

![](<../../../.gitbook/assets/Schermata 2021-11-10 alle 17.21.33.png>)

Buttons aspect can be customize by overriding the CSS classed defined in the app.css file:

```css
/* group of buttons */
.grouped-button.x-btn-over, .grouped-button-dark.x-btn-over{
    box-shadow: inset 0 0px 0px rgba(0,0,0,.075), 2px 0px 2px rgba(80, 163, 237, 0.7);
}
.grouped-button, .grouped-button-dark, .error-button, .success-button{
    background: transparent;
    border-width: 2px !important;
}
.grouped-button button, .grouped-button-dark button, .error-button button, .success-button button{
    font-weight: bold !important;
    font-size: 14px !important;
    text-decoration: none !important;
    padding: 1px 10px !important;
}

.grouped-button{
    border-color: #50A3ED !important;
    background: transparent !important;
    margin: 0px !important;
}
.grouped-button button{
    color: #50A3ED !important;
}
.grouped-button.x-btn-pressed{
    background: #50A3ED !important;
}
.grouped-button.x-btn-pressed button{
    color: white !important;
}

.grouped-button-dark{
    border-color: #1E70B7 !important;
    background: transparent !important;
}
.grouped-button-dark button{
    color: #1E70B7 !important;
}
.grouped-button-dark.x-btn-pressed{
    background: #1E70B7 !important;
}
.grouped-button-dark.x-btn-pressed button{
    color: white !important;
}



.switch-left{
    position: relative;
    border-right: 0 !important;
    margin-right: 0px !important;
    border-top-right-radius: 0 !important;
    border-bottom-right-radius: 0 !important;
}

.switch-left.x-btn-over{
    border-right: 0;
}

.switch-right{
    position: relative;
    left: -5px;
    border-left: 0 !important;
    background-color: white;
    margin-left: 0 !important;
    border-top-left-radius: 0 !important;
    border-bottom-left-radius: 0 !important;
}
.switch-middle{
    position: relative;
    left: -5px;
    margin-right: 0px !important;
    margin-left: 0px !important;
    border-radius: 0 !important;
}
```

#### Combo buttons

Additional properties to set:

* Group name: the same for the 3 buttons
* Group style: Combo for the 3 buttons

![](<../../../.gitbook/assets/Schermata 2021-11-10 alle 17.24.50 (1).png>)

#### Buttons aligned to the right

Additional properties to set:

* Alignment: Right for the 2 buttons

![](<../../../.gitbook/assets/Schermata 2021-11-10 alle 17.27.22.png>)



#### Buttons rendered as links

Additional properties to set:

* Alignment: Right for the 2 buttons
* Button type: Link for the 2 buttons

![](<../../../.gitbook/assets/Schermata 2021-11-10 alle 17.26.47.png>)

Buttons aspect can be customize by overriding the CSS classed defined in the app.css file:

```css
.button-link  {
    background: transparent !important;
}
.button-link button {
    background: transparent !important;
    color: #1E70B7 !important;
    font-weight: bold !important;
    text-decoration: underline;
}
```



