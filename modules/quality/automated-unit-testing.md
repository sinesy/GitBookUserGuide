# Automated unit testing

Unit testing is a software testing method by which individual units of source code (e.g. server-side javascript/GAE actions) are tested to determine whether they are fit for use.

When a developer is creating a server-side javascript/GAE action, he is free to organize the content as he wish. A good way to organize the content is by splitting up code into functions declarations.

Look at these two examples:

1\) all code is in-line:

```javascript
var companyId = "00000";
var siteId = 100;
var userCodeId = "ADMIN";

// reading users
var json = utils.executeQuery(
  "SELECT * FROM PRM01_USERS where COMPANY_ID=? AND SITE_ID=? AND USER_CODE_ID=?",
  null,
  false,
  true,
  [companyId,siteId,userCodeId]
);
var list = JSON.parse(json);

var total = list.length;

utils.setReturnValue(JSON.stringify({
    num: total,
    success: true
}));

```

2\) code is splitted up in declared functions; then these are invoked:

```javascript

function listaUtenti(companyId,siteId,userCodeId) {
    var json = utils.executeQuery("SELECT * FROM PRM01_USERS where COMPANY_ID=? AND SITE_ID=? AND USER_CODE_ID=?",null,false,true,[companyId,siteId,userCodeId]);
    var list = JSON.parse(json);
    list.push(user);
    return list;
}

function totale() {
    return listaUtenti("00000",100,"ADMIN").length;
}

utils.setReturnValue(JSON.stringify({
    num: totale,
    success: true
}));

```

The second one is easily testable, since the code has been organized in a TDD (test driven design) approach, i.e. first the developer thought about the portions of code to test before writing code within the declared functions.

In this way, functions can be tested separately and in a specific order.

Platform provides a new folder to prepare unit tests:

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

The first time the folder is opened, Platform proposes 2 fixed methods:

* **setUpBeforeClass** (as in JUnit),  where the developer can include js code to initialize the test case: it will be invoked by Platform before executing the xxxMethodName functions
* **tearDownAfterClass** (as in JUnit),  where the developer can include js code to remove data or anything else at the end of the test case: it will be invoked by Platform after executing the xxxMethodName functions

In addition, there is a **xxxMethodName** function, for each method found in the server-side js action.

The last button in the toolbar allows to execute manually the unit test and a dialog is prompted at the end to report the results.

Moreover, the list of actions is updated with the outcome of the test execution (red vs green).

![](<../../.gitbook/assets/image (9).png>)

Note that an empty cell means that there is not a unit test defined.

The **coverage** column represents the coverage of the source code (number of functions under test).

When defining a unit test, it is a good practice to specify a **collection**, in order to group together unit tests related to similar functionalities.

Finally, you can schedule the execution of all unit tests belonging to the same collection: in this way, you can update the outcome on a daily basis.

If you define also a notification, it is possible to receive an email reporting all outcomes.

Example of notification:

```
In data :DATE sono stati eseguiti i test automatici per l'applicazione Platform Web 6.0.2 
<br/> 
<br/> 
<br/> 
Report dei test eseguiti: <br/>
 :EXIT_MESSAGE <br/> 
 <br/> 
 <br/> 
 <center><i>Questo è un messaggio automatico. Non rispondere a questa email. </i></center>

```

The predefined :EXIT\_MESSAGE variable would generate HTML code containing the report of all unit test executions.





