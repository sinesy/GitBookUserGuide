# Service tasks

A service task represents an automatic activity, carried out automatically by the BPM engine.\
A few utility classes are provided by 4WS.Platform, in order to make it easier and faster the definition of complex processes including SQL statements to execute for reading or writing data into a database or to call a web service available in 4WS.Platform or in another web server.

Once dropped a Service Task, open its property inspector and choose the "Class" property: here you have to select among 3 alternatives: defining a Web Service, a Sql Query (reading operation) or a Sql Statement (writing operation).

Independently of the option chosen, you have to fill in a few properties, through the "Class Fields" property:

![](<../../../../.gitbook/assets/image (22).png>)

According to the Class selected, different propertied must be defined in the window above. See the sub-sections Web Service, SQL Query and SQL statement for additional details.

