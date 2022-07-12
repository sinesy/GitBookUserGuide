# Trigger writing operations

A writing operation on a relational **database** is either an **insert** or an **update** or a **delete**.

These operations can be carried out in a variety of different ways:

* using an editable **grid** and its toolbar; through a grid it is possibile to insert a list of new records, update a list of modified records, delete the selected rows
* using an **form** panel and its toolbar; through the form it is possible to create a new record, update it, delete it
* using 3 server-side javascript built-in functions: **utils.insertRecord, utils.updateRecord, utils.deleteRecord**
* using a generic DML statement, using utils.executeSql(..) built-in function

Except for the last case (executeSql), Platform provides a mechanism to listen for writing operations and automate the creation of elements to enqueue in specific queues, in order to process additional asynchronous business logic, each time a record is written in some way.

Platform provides a two-step feature to listen to writing operations and enqueue elements:

* defining **"cached" rules** to describing when and where to enqueue
* an **orchestrator**, actually using the cached rules, combined with the input data (when writing data) to figure out the enqueuing logic.



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

In this way, the orchestrator can use the operation type, written data and table to decide what to do. Moreover, the cached "Writing rules" can drive the orchestrator to work dynamically according to such rules.

Optionally, for update only operations, when the "Retrieve record before update" has been selected, it is possible also to drive the orchestrator by comparing previous and new values for the written records.



"Javascript after writing" limitations:

* you cannot include complex business logic consuming a large amount of code: no more than 2000 characters are allowed; if you are defining a complex logic here, it means you have not understood the correct design and use of this feature: complex rules are defined and cached through "Writing rules"; here there is only a simple engine
* utils.xxx methods are very limited: debug, info, warn, error, setReturnValue, stringify; again, if you need SQL methods too, it means you are not using this faeture correctly.



###

### Example for writing operations orchestrator

Let's have a table containing a series of dynamic rules:

![](<../.gitbook/assets/image (20).png>)

The "Writing rules" action would read such rules and index them for company id and returns them to cache the whole content:

```
var json = utils.executeQuery(
    "SELECT * FROM ROUTING_RULES WHERE TABLE_NAME='ABI_CAB' ",
    null,
    false,
    true,
    []
);
var rows = JSON.parse(json);

var companies = new Object(); 
/*
{

  "00000": [{
      system: ....
  }]

{
*/
for(var i=0;i<rows.length;i++) {
    var c = companies[rows[i].companyId];
    if (c==null) {
        c = [];
        companies[rows[i].companyId] = c;
    }
    c.push(rows[i]);
}


var res = {
    companies: companies
};

utils.setReturnValue(JSON.stringify(res));
```

After doing it, the cached data would be all attributes passed forward, i.e. "**companies**" attribute, which will be available as input data to the orchestrator.

The last step is defining the orchestrator, using this cached data to decide which elements to enqueue:

```
// input data:
// vos
// oldVos (for update operations only)
// companies
var queues = [];

if (companies) {
  for(var i=0;i<vos.length;i++) {
    // for each object in input
    var vo = vos[i];
  
    var entries = companies[vo.companyId];
    if (entries) {
	// there are rules for the current company in input
	utils.debug("Found "+entries.length+" rules.");

	for(var k=0;k<entries.length;k++) {
	  // for each rule found
	  var e = entries[k];
	  var toSkip = false;
	  if (e.filters) {
		 var ff = e.filters.split(",");
		 for(var j=0;j<ff.length;j++) {
		   var w = ff[j].split("=");
		   if (vo[w[0]]!=w[1])
			 toSkip = true;
		 }
	  }
	  utils.debug("e.filters "+e.filters+" toSkip: "+toSkip);
	  if (!toSkip) {
		if (e.changedFields && oldVos) {
		  toSkip = true;
		  var ff = e.changedFields.split(",");
		  var oldvo = oldVos[i];
		  for(var j=0;j<ff.length;j++) {
			if (oldvo[ff[j]]!=vo[ff[j]])
			  toSkip = false;
		  }			 
		}
		
		if (!toSkip)
		  queues.push({
		    queueName: "MYQUEUE", // can come from "companies"
		    actionId: 1489, // can come from "companies"
		    payload: vo // it would be better to pass the PK only
		  });
	  }
	}
    }
  }
}
utils.setReturnValue(JSON.stringify(queues));



```

