# Web service

A service task can act as a web service caller by setting the folllowing task properties in this way:\
Id and Name: they identity the task and they are mandatory; be sure NOT to include accent characters in these fields (only alphanumeric characters are allowed).



* Documentation: an optional description of this task
* **Class**: **it.sinesy.activiti.services.ExecuteComponentServiceTask**

You can simply select the corresponding value from the combobox: "Platform Web Service":

![](<../../../../.gitbook/assets/image (23) (1).png>)

* **Class fields**: in this list of fields, a set of properties must be defined, in order to correctly define the web service invocation:
  * name: property name to refer
  * string value: value to assign to that property
  * expression: optional expression to set, e.g.\
    ${VARIABLE == ’Test’ ? YES : ’NO’}

You can simple define the following name-value properties:

![](<../../../../.gitbook/assets/image (19) (1).png>)

A typical web service invocation available within 4WS.Platform would contain the following couples name-value, as in the picture above:

* name = **applicationId**
* string value =
* name = **companyId**
* string value =
* name = **url**
* string value = [getList?param1=val1](http://host/:port/platform/getList?param1=val1)**\&amp;**param2=val2

**Important note:** do not add the full URL, including "http://..." because you would create a workflow working only on the environment. In order to make it working in any environment, define exclusively related URLs, i.e. URL starting with the web service name (e.g. executeJs, getlist, etc.)

**Important note:** pay attention to the URL definition: the Activiti workflow editor does not allow you to write the & symbol: if you do it, it is likely that the Service Task properties will not be opened any more; for each & to include in the URL definition, use

```
&amp;
```

A more detailed example related to the invocation of the executeJs service available in Platform is:\
ClassFields\
url = [executeJs?applicationId=XXX\&appId=XXX\&actionId=xxx\&userId=ADMIN](http://host/:port/platform/executeJs?applicationId=XXX\&amp;appId=XXX\&amp;actionId=xxx\&amp;userId=ADMIN)\
httpMethod = POST\
companyId = XXXXX\
applicationId = XXX

Note that **no credentials are required** in this kind of communication, since the utility class referred is automatically able to authenticate in 4WS.Platform, starting from the user currently associated to the Activiti process, since both products share the same identity management system (users and roles).

Optional parameters:

name = requestBody\
string value = { "attr": value, … }

name = httpMethod\
string value = GET | POST | …

name = username\
string value =

name = fireError\
string value = Y

**Important note**\
In order to make more portable a process, the defined tasks should not contain references to a specific environment, such as an host or port when invoking URLs in web services.\
This goal can be reached by omitting the whole URL and use a relative URL instead.\
This simplification can be done only if the first fixed part of any URL ([http://host:port/webcontextofPlatform](http://host/:port/webcontextofPlatform)) has been defined as an installation parameter in Activiti-Rest db.properties file, where the "baseUrl" property must be set with that value.\
In this way, every installation would have its own ad hoc absolute path and all processes would remain portable, since they would not contain any more absolute URLs.



In case your service activity requires a **feedback**, you have also to:

* define a 4th parameter in Class Fields, named "**return**" and filled in with the process property name hosting the feedback
* use the **utils.setReturnValue(...)** instruction on the js server-side action to provide such a feedback

A few constraints must be respected:

* the feedback MUST always be expressed as a JSON string
* if you need to work with attributes coming from the JSON string, you'd better postpone a **Script activity** to the Service activity, in order to extract the JSON attributes and set each of them as a process property.

Example:

![](<../../../../.gitbook/assets/image (24).png>)

The Service activity has a Class Field property named "**return**", filled with "**RESPONSE**", i.e. "RESPONSE" would be the javascript object hosting the response coming from thr js server-side action, which would give back a JSON string.

The js server-side action MUST give back something like:

```
var response = {
    outcome: outcome
};
utils.setReturnValue(JSON.stringify(response));
```

The Script activity must be defined as:

* Script format: "JavaScript"&#x20;
* Script:

```
execution.setVariable("OUTCOME", execution.getVariable("RESPONSE").outcome);
```

In this way, the JSON string coming from the js server-side action would be converted internally in a js object and the instruction above will extract the attribute "outcome" from the "RESPONSE" js object and store the attribute value to the "OUTCOME" process property.

Any other part of the workflow will be then able to access to the OUTCOME process property.

**Note**: it is possible that such variables are not reported in the Instance process execution or History screens.

## Example

| … baseUrl=[http://localhost:8180/platform/](http://localhost:8180/platform/) … |
| ------------------------------------------------------------------------------ |

value of "url" class property within a web service Service Task:

| executeJs?applicationId=XXX\&appId=XXX\&actionId=xxx\&userId=:ADMIN |
| ------------------------------------------------------------------- |

**Important note**\
Do NOT use the notation ${VARNAME} in the definition of a web service: you have to use the notation :VARNAME instead.
