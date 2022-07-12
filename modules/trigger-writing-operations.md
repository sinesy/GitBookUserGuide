# Trigger writing operations

A writing operation on a relational **database** is either an **insert** or an **update** or a **delete**.

These operations can be carried out in a variety of different ways:

* using an editable **grid** and its toolbar; through a grid it is possibile to insert a list of new records, update a list of modified records, delete the selected rows
* using an **form** panel and its toolbar; through the form it is possible to create a new record, update it, delete it
* using 3 server-side javascript built-in functions: **utils.insertRecord, utils.updateRecord, utils.deleteRecord**
* using a generic DML statement, using utils.executeSql(..) built-in function

Except for the last case (executeSql), Platform provides a mechanism to listen for writing operations and automate the creation of elements to enqueue in specific queues, in order to process additional asynchronous business logic, each time a record is written in some way.

In order to do it, you have first to open the data model definition for a relational database table.&#x20;

![](<../.gitbook/assets/image (22).png>)

In such a scenario, there are 3 additional input controls to use in order to activate the writing operations listening:

* **Writing rules** - this combobox allows to select a server-side javascript action, which will be invoked once by Platform and used to gather all information needed to decide how to manage each subsequent writing operation; the action must return such a configuration, using utils.setReturnValue() which must return a JSON string containing all the logic to figure out how to manage an insert, an update or a delete. This JSON string will be automatically cached by Platform behind the scenes. This cache is maintained at maximum for a minute: in this way, in case of a cluster environment with a dev changing this "Writing rules" action or the "Javascript after writing", the cache will be refreshed. In case of a non cluster environment (like a development environment), the cache is instantly refreshed when the action is replaced or the "Javascript after writing" content has changed.
* **Retrieve record before update** - this is an optional checkbox and **it is strongly recommended NOT TO select it**, if not needed, because it involves an additional workload for every update operation. When checked, before each UPDATE writing operation there will be a SELECT query first, in order to get the previous content of the record, before updating it. This previous state will be passed forward to the "Javascript after writing" router, so that there can be a business logic which can compare specific attributes to check out which one have been changed and enqueue or not according to which ones have changed.
* **Javascript after writing** - the purpose of this javascript code (no more than 2000 characters) is just to define in which queues to enqueue the data change, so from this perspective it is working as an **orchestrator**. It is allowed to enqueue the event in multiple queues: the return value is  a JSON string representing an array of queues to use, having the format:&#x20;

```
[{ 
  queueName: "...", 
  payload: {...},
  actionId: ...,
  note: "..." // optional
 },
 ...
 ]
```

In order to figure out which queues to manage, this orchestrator receives in input the following content:

```
var operation = "..."; // "insert" or "update" or "delete"
var oldVos = [...]; // only for operation = "update" and the "Retrieve record before update" checkbox selected
var vos = [...]; // the list of records written
var tableName = "..."; // the table where the writing operation has been executed
var ... // all other objects returned by the "Writing rules" cache
```

In this way, the orchestrator can use the operation type, written data and table to decide what to do. Moreover, the cached "Writing rules" can drive the orchestrator to work dinamically according to such rules.

Optionally, for update only operations, when the "Retrieve record before update" has been selected, it is possible also to drive the orchestrator by comparing previous and new values for the written records.







