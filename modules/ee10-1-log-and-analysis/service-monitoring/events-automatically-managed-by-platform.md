# Events automatically managed by Platform

Platform can generate automatically a series of messages, each with a specific log level; the following table reports the event and its corresponding level:

| **Event** | **Log level** |
| :--- | :--- |
| an HTTP error programatically fired by a Platform developer using the “utlis.setHttpResponseCode” method \(\*\) | ERROR |
| a lock database error is fired by the database and intercepted by Platform, when executing a server-side javascript action \(\*\) | FATAL |
| an out of memory error is fired by the Application Server and intercepted by Platform, when executing a server-side javascript action \(\*\) | FATAL |
| any other error within a server-side Javascript action, not programatically managed by the Platform developerthrough the try {} catch {} | ERROR |
| authentication error when trying to invoke a web service \(server-side Javascript action\) from an external system \(\*\) | ERROR |
| an out of memory error is fired by the Application Server and intercepted by Platform, when executing an export from tables job \(\*\) | FATAL |
| any other error within the export from tables job \(e.g. connection timeout, too many connections, etc.\) | ERROR |
| an out of memory error is fired by the Application Server and intercepted by Platform, when dequeuing an action from a queue \(\*\) | FATAL |
| any other error intercepted by Platform, when dequeuing an action from a queue \(e.g. connection timeout, too many connections, etc.\) | ERROR |

\(\*\) a message code is also generated; consequently, the Knowledge Base can provides details about such an error. See the Knowledge Base section for detailed information.

**Note**: FATAL errors have the chance to be re-executed later with a successful outcome, since the error was not caused by the input content, rather by a transitory bad internal state \(out of memory, database, etc.\).

