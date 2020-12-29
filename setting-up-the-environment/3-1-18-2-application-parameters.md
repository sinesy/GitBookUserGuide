# Application parameters

When opening the detail window of a new application, there are two folders available: one contains the settings for the selected application, the other the application parameters, which is an editable grid, where the user can add, change and delete common parameters.  
When saving parameters, these will be accessible from an application when the user will re-logon to the application.  
These parameters are used by specific functionalities of the interpreted application and they are reported in the following list:



### 4WS.PLATFORM

**Starting web page** - URL representing the base URL of this Platform installation; it is recommended to set it up, since it is used widely by Platform, for example when sending emails containing references to this server.

Example: 

https://yourhouse/platform/

**Last export** - do not change it; it is automatically defined by Platform, each time a metadata export has been carried out. Helpful to compare two versions of the same app, installe din different environments \(e.g. development vs production\)

**Last import** - do not change it; it is automatically defined by Platform, each time a metadata import has been carried out. Helpful to compare two versions of the same app, installe din different environments \(e.g. development vs production\)

**List of enabled component ids \(comma separated\)** - helpful when the checkbox parameter "PERMISSIONS -&gt; Check function Ids when reading data \(Y/N def. N\)" has been activated; there can be business components not directly connected to grids/forms/selectors: in such a scenario, you can refer here all component ids related to business components invoked manualy by getlist/getdetail invocations from the UI; if not reported here, there will be "unauthorized" errors when trying to invoke these components.

**Last GAE export** - do not change it; it is automatically defined by Platform, each time a metadata export to "Platform for GAE" has been carried out. Helpful to compare two versions of the same app, installe din different environments \(e.g. development vs production\)

**Customize Mapping** - can be either an action id or a full java class name \(namespace included\); if set, the action/java class will be invoked each time the application has defined objects with different mappings, i.e. an object representing different tables in different database schema; this class is invoked and has to provide the right datasource id to use each time.

Example:

```javascript
/*
Available input for the invoked action:
   reqParams.fromClassName = "WAG4WSUtilityMethods";
   reqParams.dataStoreId = <default data source id defined for the current object>;
   reqParams.dataStores = [{ Con04_Additional_Datastores object },...];
   
   headers.appId = "..."; // current app id
   
   vo = { ... }; // calling component/action input vo
*/

var datasourceId = ...

utils.setReturnValue(datasourceId+""); // return the data source id to use, expressed as a String
// note: you can be "" or "0" in case you do not wanna change the default data source id
```

**Platform Lite Password** - in case you have an additional "Platform for Lite" installation, this is the password to use to communicate between this Platform Standard and the other installation, in order to export metadata.

**Platform Lite URL** - in case you have an additional "Platform for Lite" installation, this is the URL to use to communicate between this Platform Standard and the other installation, in order to export metadata.

**Screenshots Directory Id** - if filled with a directory id previously set up, it is possible to take screenshots of the interpreted web application \(for example when there is a bug\) and report it to the dev team. These screenshots will be saved in this directory. Screenshots can be taken using the "copyWebPage" global javascript function, available on the UI, which can be invoked from any point of your web UI.

**Set of allowed variables to set from client side** - in order to secure the server layer, it is a good practice not to pass forward from the UI to the server "custom" variables which can affect the server behavior, since the same client invocations could be carried out from external clients as well. 

However, when some variables are essentials and must be passed to the server, you can declare them through this parameter \(specified as a list of separated comma parameter names\) and then use the   
"wagutility/sendcustomappluservar" standard web service, which will accept in input only variables declared through the current parameter.

Do not let this parameter empty, if you have planned to pass forward variables to the server layer.

**Application Version** - you should define it each time you export changes to another environment and it represents the current application version, you can show in you About window in the interpreted mobile/web app.

**Customize Datastore** - can be either an action id or a full java class name \(namespace included\); if set, the action/java class will be invoked each time the application has defined objects \(i.e. tables\) available in different database schemas, i.e. an object representing the same table in different database schema, typical in a multi-tenancy application, where you have an ad hoc schema for each tenant and all schemas have the same tables in terms of structure but different data stored; this class is invoked and has to provide the right datasource id to use each time.

Example:

```javascript
/*
Available input for the invoked action:
   reqParams.fromClassName = "WAG4WSUtilityMethods";
   reqParams.dataStoreId = <default data source id defined for the current object>;
   reqParams.dataStores = [{ Con04_Additional_Datastores object },...];
   
   headers.appId = "..."; // current app id
   
   vo = { ... }; // calling component/action input vo
*/

var datasourceId = ...

utils.setReturnValue(datasourceId+""); // return the data source id to use, expressed as a String
// note: you can be "" or "0" in case you do not wanna change the default data source id
```

Example**:**

```javascript
if (reqParams.dataStoreId==null || reqParams.dataStoreId==0 || reqParams.dataStoreId==-1) {
    utils.setReturnValue("");
}
else {
    var json = utils.executeQuery(
        "SELECT DATASTORE_ID FROM CON04_ADDITIONAL_DATASTORES WHERE DESCRIPTION IN "+
        "(SELECT COD_SOCIETA FROM SOCIETA WHERE USERCODE_ID=:USERNAME)",
        null,false,true,
        []
        );
    var list = eval("("+json+")");
    if (list.length==1) {
        utils.setReturnValue(list[0].datastoreId);
    }
    else {
        utils.setReturnValue("");
    }
}
```

**Last context import** - do not change it; it is automatically defined by Platform, each time a web context import has been carried out. Helpful to compare two versions of the same app, installed in different environments \(e.g. development vs production\)

**Notify action editing** - checkbox  

**Manually loaded Digest** - checkbox used in a cluster environment to speed up the web interpreted application; when selected, all metadata and user data \(when a user is logging on\) is cached internally, so the number of SQL queries is significantly reduced. 

Bear in mind that if you select it, you have to clear cache manually on each cluster node, each time you apply a change on metadata or when you import metadata. You can do it through the "Administration -&gt; Force digest update" menu item.

For more details see:

{% page-ref page="3-1-18-2-application-parameters.md" %}

**Hide toast message with alert messages \(def. N\)** - checkbox used to change the default behavior of the Alert functionality, i.e. showing a toast message each time an alert arrives on the UI. When checking this parameter, the toast message is omitted.

**Show a popup message for the chat \(Y/N\)** - checkbox used to change the default behavior of the Alert functionality, which does NOT include any dialog message each time an alert arrives on the UI. When checking this parameter, the dialog message is showed. It would make sense to use only one of the two alternative described here: either the toast message or the dialog message. 

**Do not allow to pass a SQL filter on panel loading** - checkbox used to block any additional condition when invoking the standard web service getlist, used to fetch a list of records \(for a grid or a selector\). If not checked, it is allowed to pass a SQL fragment to the base SQ query executed on the server side, which would represent a SQL injection risk.

It is strongly recommended to select it.

If you have SQL based business components which work with additional SQL filters, you can fix this situation using the following steps:

* replace the SQL based business component with a JS business component
* copy the same base SQL query in the new component, using utils.getPartialResult
* embed within the new component any custom logic thast previously you defined using addional SQL filters.

**Take into account the difference between UTC and GMT for datetime** - checkbox used to change the date+time value to show in grids/forms, by taking into account the time zone difference between the client and the server.

It is strongly recommended to select it.

**Take into account the difference between UTC and GMT for date** - checkbox used to change the date value to show in grids/forms, by taking into account the time zone difference between the client and the server.

It is strongly recommended to select it.



### ACTIVITI

**Tomcat Path of Activiti** - the absolute path to set, related to the installation of Activiti within a Tomcat.

Example: 

/opt/tomcat-activiti/

**Base Rest URL of Activiti** -  base URL of Activiti; it can be an internal URL not a public URL.

Example:

[http://localhost:8280](http://localhost:8280)

**Base Designer URL of Activiti** - base URL of Activiti, used to access Activiti Explorer \(i.e. the BPM designer\); it must be a public URL.

Example:

http://host/



### ALERT

**Alert message template** - optional text

**Show title in the alert message list \(def. N\)** - checkbox used to show/hide the title of the message in each alter message arrived

**Disable click on alert message \(def. N\)** - checkbox used to ignore the click of an alert message and NOT mark it as read

**List of commands to include in the alter dialog** - optional JSON string, containing a list of commands to add. For more details:

[https://4wsplatform.gitbook.io/knowledge-base/how-to-customize-the-alert-message-content](https://4wsplatform.gitbook.io/knowledge-base/how-to-customize-the-alert-message-content)



### ALFRESCO

Alfresco: base dir for folders explorer - 

Alfresco: URL when connecting to Alfresco Server - 

Alfresco: sync roles in Alfresco \(Y/N\) - 

Alfresco: sync users in Alfresco \(Y/N\) - 

Alfresco: Admin Password when connecting to Alfresco Server - 

Alfresco: Admin Username when connecting to Alfresco Server - 

Alfresco: model file name when connecting to Alfresco Server - 

Alfresco: sync user roles in Alfresco \(Y/N\) - 



### ARCHIFLOW

ARCHIFLOW\_DOMAIN - 

ARCHIFLOW\_BASE\_URL - 

ARCHIFLOW\_LANGUAGE - e.g. 0

ARCHIFLOW\_PASSWORD - 

ARCHIFLOW\_USERNAME - 

ARCHIFLOW\_DATE\_FORMAT - e.g. dd/MM/yyyy



### **AUDIT**

**Days for keeping data logs** - it is strongly recommended to set it, when there is at least one object managed using the audit. In such a case, it is important to automatically remove collected data automatically, to avoid to fill in the database with a large amount of data. A good value can be 365 \(days\) or less.



### COLLABORATION

Collaboration



### CONTACTS\_SYNC

Contacts synchronization sources \(4WS, LDAP, GOOGLE,...\)



### GOOGLE

**Password Platform for GAE** - this parameter must be set in case there is a Platform for GAE installation connected to the current Platform Standard Edition: in such a scenario, metadata defined through the App Designer must be sent to GAE, where it will be used to run the web services layer in the high scalable GAE web container. In order to sent metadata to Platform for GAE, you have to fill out this parameter, with the value set in the Application entity of Google Datastore.

**Google Analytics Id** - in case of mobile apps, this parameter can contain the Google Analytics project id connected to the mobile app, so that events generated by the app cam be sent and collected into Analytics.

**Google SSO**: needed OAUTH scopes \(white space separated list. See [https://developers.google.com/identity/protocols/googlescopes](https://developers.google.com/identity/protocols/googlescopes)\)



### JIRA

**Jira URL** - URL to Jira Server or Jira Cloud, related to a specific tenant

**Jira project Id** - id for the activated tenant in Jira



### LDAP

**LDAP port \(opt. def. 389\)** - LDAP port, typically the default 389 port

**LDAP checking enabled \(opt. def. true\)** - can be either true or false, according to the LDAP settings

**LDAP server** - IP or server name of the LDAP server

**LDAP protocol** \(ldap or ldaps. Opt. def. ldap\) - protocol to use when connecting to the LDAPO server; a typical value is "ldap", but you have to use "ldaps" in case of LDAP over SSL communication

**LDAP: Password** to use when connecting to LDAP 

**LDAP: Username** to use when connecting to LDAP 

**LDAP account auth format** \(e.g. {u}@domain\) - example: {u}@sinesy.it

**LDAP: Query page size** \(opt. default 1000\) - set it in case the LDAP contains a large amount of users \(more than 1000\) and the user reading process could slow down because of the amount of users to read: in such a case, it would be better to set a pagination size of 100 or more; this parameter is used by Platform only if "Activate pagination" parameter is set to true

**LDAP: Base path when searching for users** - example: ou=xxx,dc=yyy,dc=zzz

**LDAP: Base path when searching from groups**  - example: ou=xxx,dc=yyy,dc=zzz

**LDAP: Field types** to manage in groups \(opt.\) 

**LDAP: Fields** to manage in groups \(opt.\) 

**LDAP: Groups filter** \(opt.\) 

**LDAP attribute for user id** \(opt.\) DEPRECATED: Autoassign roles to new LDAP user \(';' separated list - see PERMISSIONS section\) 

**LDAP: Group key attribute** \(opt.\) 

**LDAP: Activate pagination** \(true or false, opt., def. true\) - set it to true to read users a page a time \(see "Query page size" parameter\)

**LDAP: Query result limit** \(opt. default none\) - set it to limit the maximum amount of users to read

**Action Id to use on login** to replace the username - helpful to define a username for Platform to use instead of the one retrieved by the LDAP server, for example to extract the left part of an email address and use it as the username

SYNC\_LDAP\_GROUP\_UNIQUE\_NAME



### LOGS

**Max days to log** - this parameter is related to the Table Log, i.e. log saved to CON60\_LOGS table.

It is essential to put a limit to the log events to save here. Please always set it, for example to 60 \(days\).

**Max days to log per Type \(e.g. QUEUE=1,JS\_ERROR=1\)** - this is more detailed than the previous parameters, where you can distinguish among each even type; you can define the max amount of days for each log type, by separating them using the comma.

Available log types are:

* QUEUE - a message logged when an element extracted from a queue has been processed, but only in case of calls like: utils.enqueueAction\(....,true\)
* JS\_ERROR - a message logged in case of errors when executing a server-side js action \(a js/java exception not managed\)
* ALERT - a message logged in case of an alert message
* SMS - a message logged in case of SMS messages sent
* EMAIL - a message logged in case of email messages sent
* MOBILE\_ERROR - a message logged in case of errors within the mobile app
* CENTRAL\_SYNC\_ERROR - a message logged in case of errors when synchronizing a mobile app
* APP\_ANALYSIS - a message logged each time the app is analyzed
* NETTEST - a message logged each time a user executes the network test
* TEST - a message logged each time an automated test is executed
* EXPORT\_TABLE - a message logged each time an "export from table" is executed
* APP\_EVENT - a message logged each time an application event is fetched \(e.g. login, out of memory, etc.\)



### LOGIN

Enabled users

Version of Login Form

Show combos for Company and Site \(YN\)

Login label in controls

Access Unavailable message

Translate login labels with browser language



### MAIL

SMTP host when sending email

SMTP port when sending email \(opt.\)

SMTP username when sending email \(opt.\)

SMTP password when sending email \(opt.\)

Use TLS when sending email: E/F \(opt.\)



### MAPS

Google Maps: Start Point Latitude

Google Maps: Start Point Longitude

Google Maps: Start Point Name

Google Maps: Do not set a default position



### MOBILE

Fee-paying mobile app \(Y/N def. N\)

Google key for autocomplete place in iOS

Google key for autocomplete place in Android



### PERMISSIONS

Show role id \(Y/N\)

Login controls to hide exit Check function Ids when reading data \(Y/N def. N\)

Show only enabled roles

Autoassign roles to new user \(';' separated list\)

Default value for login controls



### REPORTS

Remote reports Server URL



### SCHEDULER

From email address when sending email from Scheduler



### SECURITY\_SYNC

Destinations for the sync process groups/users

Sync users \(true/false def. true\)

Sync also groups \(true/false\) \(opt.\)

Sources for the sync process groups/users



### SMS

Email suffix when sending SMS

From SMS Phone Nr

Default International prefix for SMS

Twilio SMS Account SID

Twilio SMS Auth Token



### SSO

Authentication chain \(opt. def. '4ws'\)

Sync: Company,site couples to use when creating records \(opt. def. all\)

Sync: Logical delete of users before sync \(opt. def. false\)

Sync: Fields to manage in 4WS users table \(opt.\)

Sync: Fields to manage in 4WS groups table \(opt.\)



### TENSOR FLOW

TensorFlow password

TensorFlow url



### UI

Single Document Interface \(Y/N\) \(predef. N\)

Application icon

Menu levels 1

Show window icon \(Y/N\)

Context help

Top bar height \(pixels\) 60

Enable menu file \(true/false\)

Favourite icon suffix

Popup windows with closing button \(def. N\)

Menu tree width

Modal windows with closing button \(def. N\)

Enable menu filter \(true/false\)

Status bar height \(pixels\)

Use default icon for user profile when not found \(def. N\)

Order of Grid Export

View asterisk on mandatory controls \(Y/N\) \(default N\)

Message for empty panel

First level menu height \(pixels\) 0

Second level menu height \(pixels\)

Grid in edit with double click \(YN\) \(default N\)

Show alert in menubar \(Y/N\)

Hide icons in tabs menu \(Y/N\)

Text filter by enter \(Y/N\) \(default N\)

Show short unique key

Toolbar buttons expand \(Y/N\) \(default N\)

Loading order of the context css files Default

Read CSS context files only from css/css\_login folders

View asterisk on mandatory controls only when needed \(Y/N\) \(default N\)

Label position of Designer functionality



### USERS

Supported user languages Component Id 69

Action id \(JSServer\) to use after change password

Action Id \(server-side js\) to be performed after insert/update/delete a user

Flag used to hide the warning message when saving user roles \(def. N\)

Action Id \(server-side js\) to take before you insert/update/delete a user

Action id \(JSServer\) to use after application user logout



### VOICE

Activate voice synthesize \(Y/N, def. N\)

Start voice command \(e.g. platform\)



### WHATSAPP

**Secret key** - required as well as "account id": the value is defined in the Twilio Whatsapp Admin Console

**Phone number used as sender** - the phone number to use when sending email; it is required and to define first in the Twilio Whatsapp Admin Console

**Action id for Whatsapp callback** - optional value: if set, it is a server-side action, defined as PUBLIC web service \(i.e. no credentials are required when invoking it\); this field is needed only in case you want not only send Whatsapp messages but also get feedbacks, like "message sent" or "message read": this is the callback ws which receives these events from the Whatsapp service.

**Account id** - required as well as "secret key": the value is defined in the Twilio Whatsapp Admin Console







## 

