# How to start a process from a JavaScript action

var processInstanceId = **startActivitiProcess** (processId, obj);

* processId: process id

This value can be retrieved from the list of the processes or from the Web Modeler. Example: in the "Execution process list" you can see all the processes. To be more precise, all the versions for all the processes, where a specific process version is expressed as:\
SIN\<YOUR_COMPANY\_ID>\_YOUR\_COMPANY\_ID>_\<YOUR_PROCESS\_ID>:\<VERSION>:\<INTERNAL\_ID>_\
_The processId to specify must NOT include version and internal id, so it must be something like:_\
_SIN\<YOUR\_COMPANY\_ID>\_YOUR\_COMPANY\_ID>_\<YOUR\_PROCESS\_ID>

* obj: Javascript object containing variables declared in the start event and required in order to start the process.

More precisely, if you have defined variables like MY\_EMAIL\_ADDRESS and MY\_NAME, then the javascript object should contain something like:\
{ myEmailAddress: “…”, myName: “…” }\
that is to say, variable names must be expressed in "camel-case".

Note: the **start** variable is a boolean value representing the outcome of the process start.

## Example

```javascript
var obj = {
  requestDate: new Date(),
  docId: vo.documentId,
  requestId: vo.requestId,
  initiator: vo.requestUserId
};

var processInstanceId = null;
try {
  processInstanceId = startActivitiProcess("PROCESS_ID",obj);
}
catch(e) {
  // in case of failure when attempting to start a process, an exception is fired here: e.toString() contains the error message
}
```
