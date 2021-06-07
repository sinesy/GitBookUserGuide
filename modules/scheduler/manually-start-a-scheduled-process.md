# Manually start a scheduled process

A scheduled process should always be started by the scheduler sub-system and not manually.

Anyway, it is possible to manually start a scheduled process, using a server-side javascript function:

```text
var json = utils.maybeStartProcess(Long schedId,Boolean forceRunning,Boolean startNextProcesses);
```

**Syntax**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Argument</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">schedId</td>
      <td style="text-align:left">scheduler identifier, visibile in the scheduled process list, used to
        uniquely identify the process to start manually</td>
    </tr>
    <tr>
      <td style="text-align:left">forceRunning</td>
      <td style="text-align:left">if set to true, the process will start, independently of currently process
        under execution; if set to false, the process starts only if there is NOT
        a process running yet. It is strongly recommended to set this argument
        always to false, in order to avoid dangerous multiple executions of the
        same process (the concurrent access to resources can lead to database locks,
        writing file with wrong content, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">startNextProcesses</td>
      <td style="text-align:left">if set to true, at the end of the current process execution, children
        process will be automatically started</td>
    </tr>
    <tr>
      <td style="text-align:left">json</td>
      <td style="text-align:left">
        <p>This function returns always a JSON string, having the following content:</p>
        <p>{</p>
        <p>success: true|false,</p>
        <p>errorCode: &quot;...&quot;,</p>
        <p>exitCode: &quot;...&quot; ,</p>
        <p>exitMessage: &quot;...&quot;</p>
        <p>}</p>
      </td>
    </tr>
  </tbody>
</table>

In case of correct start of the process, the JSON would return 

**{ success: true, exitCode: "..", exitMessage: "..." }**

In case of invalid "schedId" argument, the JSON would return 

**{ success: false, errorCode: "NOT\_FOUND" }**

In case of a process currently running and the "forceRunning" argument se to false, the JSON would return 

**{ success: false, errorCode: "ALREADY\_RUNNING" }**

\*\*\*\*

**Note**: the javascript function is synchronous, that is to say, it lasts as long as the process lasts.





