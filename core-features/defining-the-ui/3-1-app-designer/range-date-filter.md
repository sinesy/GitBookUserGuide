# Range Date Filter

## Range Date Filter

The range date filter is a control available in the filter and editable panels. This control can filter the associated grid for a range of dates in two ways: you can filter the date field either with "between operator" or with "between operator excluding the date limits".

In an editable panel you can use this control for selecting the start and end date for any usage.

#### Configuration and use

You can configure the control in the Input Controls folder (Range Date type) and select the "Between" or "Between (excluding date limits)" operator.

![](<../../../.gitbook/assets/image (19) (1) (1).png>)

In the application you can view a control with two calendars for the selection of the start and end date, composing the date range.

![](<../../../.gitbook/assets/image (21) (1) (1).png>)

You can set other properties through the "Additional configuration" property of a control:

**minDate** (default 1970/01/01): lower limit selectable

**maxDate** (default 2999/12/31): upper limit selectable

**showTopbar** (default false): on the upper part of the calendar you can show a top bar with three buttons for the selections of start date, end date or range date.

**showToday** (default true): show or not the Today's buttons

**format**: you can specify the date format  in the control after selection

**hideValidationButton** (default false): if true it hides the "Confirm" button

**dateSeparator** (default ' - '): you can specify the date separator in the control



If you want to set a default value you can write a string with start and end date with the specified format.

![](<../../../.gitbook/assets/image (20) (1) (1).png>)
