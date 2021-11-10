# Manually start a scheduled process

A scheduled process should always be started by the scheduler sub-system and not manually.

Anyway, it is possible to manually start a scheduled process, using a server-side javascript function:

```
var json = utils.maybeStartProcess(Long schedId,Boolean forceRunning,Boolean startNextProcesses);
```

**Syntax**

| Argument           | Description                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| schedId            | scheduler identifier, visibile in the scheduled process list, used to uniquely identify the process to start manually                                                                                                                                                                                                                                                                                                   |
| forceRunning       | if set to true, the process will start, independently of currently process under execution; if set to false, the process starts only if there is NOT a process running yet. It is strongly recommended to set this argument always to false, in order to avoid dangerous multiple executions of the same process (the concurrent access to resources can lead to database locks, writing file with wrong content, etc.) |
| startNextProcesses | if set to true, at the end of the current process execution, children process will be automatically started                                                                                                                                                                                                                                                                                                             |
| json               | <p>This function returns always a JSON string, having the following content: </p><p>{ </p><p>  success: true|false, </p><p>  errorCode: "...", </p><p>  exitCode: "..." , </p><p>  exitMessage: "..." </p><p>}</p>                                                                                                                                                                                                      |

In case of correct start of the process, the JSON would return&#x20;

**{ success: true, exitCode: "..", exitMessage: "..." }**

In case of invalid "schedId" argument, the JSON would return&#x20;

**{ success: false, errorCode: "NOT\_FOUND" }**

In case of a process currently running and the "forceRunning" argument se to false, the JSON would return&#x20;

**{ success: false, errorCode: "ALREADY\_RUNNING" }**

****

**Note**: the javascript function is synchronous, that is to say, it lasts as long as the process lasts.



