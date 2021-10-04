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

**If the following log types are not specified and only "Max days to log" is filled out, then this setting will be applied to all log types**. Consequently, if you want to set a specific limit for a specific log type, you have NOT to specify "Max days to log", but use "Max days to log per Type" instead.

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
* SQLTOOL\_QUERY - queries executed using SqlTool and part of the history available in the Sql Shell panel



### LOGIN

**Enabled users** - a list of usernames, separated by comma \(,\). When this field is filled, the log on is blocked for all users except for the ones specified here. This parameter is helpful during an application upgrade which consists of upgrading the database, importing metadata and web context. During that process, it would not be a good idea to let the end users access the application: through this parameter you can block users from accessing the app, except for the devs. Once finished and tested everything, you should clear up this parameter, so that all end users can access the app again.

**Version of Login Form** - the login page can be customized in a variety of ways; throgu this parameter you ca define how many buttons it contain, among these alternatives:

* Exit + Login Buttons
* Login + Exit Buttons

**Show combos for Company and Site \(YN\)** - checkbox used to replace the input fields for company and site with comboboxes, in roles/users details. 

**Login label in controls** - when the checkbox is selected, in the login page the labels on the left of the input fields are removed and moved within the input fields.

**Access Unavailable message** - when the "Enabled users" property is filled in, you can also show a customized message dialog when an end user attempts to access the application; through the current property you can define the text to show in this scenario.

**Translate login labels with browser language** - checkbox used to auto-set the language in the login page, according to the browser language.

**Log last login date/time \(def. N\)**  - checkbox used to enable the logging of the last date+time of a user login: each time a user is logging on successfully, the corresponding record in PRM01_USERS is updated for the fields LAST\__LOGIN and TOTAL\_LOGIN.

Note: the login time is not recorded in case of either a stateless web service login or an element in queue or a scheduled process.



### MAIL

This section is mandatory in case there are functionalities which send email messages, like an email to send with template, app diagnosys, scheduled processes which notifies by email, etc.

**SMTP host when sending email** - the host name of the SMTP server used to send email messages; this parameter is mandatory; examples: smtp.mandrillapp.com or smtp.gmail.com

**SMTP port when sending email \(opt.\)** - the port used by the SMTP server to accept email messages to send; if not specified, the default port 25 is used; bear in mind that you cannot use the default port 25 if your Platform server has been installed in the Google Cloud Platform, since this port is blocked in the GCP. Moreover, the port also depends on the protocol used: smtp or smtps \(SMTP over SSL\).

**SMTP username when sending email \(opt.\)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**SMTP password when sending email \(opt.\)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**Use TLS when sending email: E/F \(opt.\)** - allowed values are E or F, i.e. enabled or forced and it depends on the SMTP server settings: check it out with the administrator of your SMTP server.

**Email Debug** - enable the debug of messages sent/received



### MAPS

This section is used in case your application uses Google Map feature and show a google map within a "Google Map panel". In such a scenario, all these properties are required.

**Google Maps: Start Point Latitude** - default latitude coordinate to use in case the Google Map panel is not filled in with am initial coordinate. If the panel is filled in with one or more coordinates, this setting is ignored.

**Google Maps: Start Point Longitude** - default longitude coordinate to use in case the Google Map panel is not filled in with am initial coordinate. If the panel is filled in with one or more coordinates, this setting is ignored.

**Google Maps: Start Point Name** - default caption text to show for the default coordinate to use in case the Google Map panel is not filled in with am initial coordinate. If the panel is filled in with one or more coordinates, this setting is ignored.

**Google Maps: Do not set a default position** - checkbox used to set or not a default coordinate for a Google Map panel which has not been filled with a coordinate. If not checked, the default settings defined above will be used.



### MOBILE

Fee-paying mobile app \(Y/N def. N\)

Google key for autocomplete place in iOS

Google key for autocomplete place in Android



### PERMISSIONS

**Show role id \(Y/N\)** - checkbox used to define whether the role id column/control must be showed int he users list and in the user detail window. As a default setting, this information is not visible and consequently the role id is an auto-generated number reckoned by Platform behind the scenes. 

You should check this parameter only in case you want to be free to define the role id and not let Platform to generate it.

**Login controls to hide exit Check function Ids when reading data \(Y/N def. N\)** - comma separated list of input fields in the login pane to hide. For example in a Platform installation where there is one only tenant \(one only company id\) or there is only one site id, it is useless to force the end user to specify them each time he logs on and they can be hidden and pre-filled. 

This parameter allows not only to define the list of input fields to hide but also the value to preset for them.

Example:

exit,companyId=00000,siteId=100

The example above would hide the exit button, the company id input field and preset it with a value of 00000, hide the site id input field and preset it with a value of 100.

Allowed input fields that can be hidden:

* companyId
* siteId
* language
* exit

**Show only enabled roles** - used in the user detail window: if this checkbox is selected, the list of roles to show is filtered by the roles already owned by the current user; if not selected, all users can see all defined roles at application level, but can only select in the grid \(in edit mode\) the ones owned by the current user.

**Autoassign roles to new user \(';' separated list\)** - in case a user is auto-created when logging on \(e.g. when the authentication is managed externally by an LDAP server\), no roles have been assigned to him yet and consequently, it would not be possible for him to access the application, since two requirements must be fulfilled: a correct authentication + at least one role assigned to the user.

If this checkbox is selected, a user not having roles assigned yet, would inherit automatically the role \(or list of roles separated by a comma\) specified through this parameter and consequently he can access successfully the application.

**Default value for login controls** - ?



### REPORTS

Remote reports Server URL



### SCHEDULER

**From email address when sending email from Scheduler** - this parameter is essential in case you have defined scheduled processes and include also a notification email, i.e. an email address \(or more than one\) to use to send email messages according to the exit code of the scheduled terminated process. This parameter represents the "from email address" to use when sending notification emails.



### SECURITY\_SYNC

As part of the integration with external authentication systems \(SSO, LDAP, AD, Google or other federated SSO systems\), Platform offers the ability to synchronize the users and/or groups from these sources.

This operation is helpful to have the usernames defined in the LDAP also internally to Platform: only in this case you could associate roles to users. 

If a user is not defined in Platform too, it would be impossible to refer it and link to it a set of roles!  


To enable this feature, the following parameters must be set in the general configuration or the application specific configuration.  


**Destinations for the sync process groups/users** - semicolon \(“;”\) separated list of destinations to put information in. Possible values: 4WS. Default: empty list

**Sync users \(true/false def. true\)** - flag to enable or disable the synchronization of users. Possible values: “true” or “false”. Default: “true”.

**Sync also groups \(true/false\) \(opt.\)** - flag to enable or disable the synchronization of groups. Possible values: “true” or “false”. Default: “true”.

**Sources for the sync process groups/users** - semicolon \(“;”\) separated list of sources to get information from. Possible values are: GOOGLE, LDAP. Default: empty list

\*\*\*\*

**Note**: To configure more than one source per type \(LDAP1, LDAP2, …\) use this syntax: LDAP1;LDAP2. Where LDAP1/2 is the prefix of the source.

**Note:** You can automate the synchronization of users and roles, using a predefined scheduled process: the following URL must be called:

http\[s\]://secursync

  
  


### SMS

This section represents all settings needed when sending SMS messages from the App Diagnosys functionality, in case there is a notification to send to the specified address \(phone number\) and the analyzed results are sent to that address. 

Not all these settings are needed:

* if you send SMS messages through an **external SMS email gateway,** you have first of all to specify the  SMTP settings through the MAIL parameters section and then fill in here the first two parameters
* if you send SMS messages through the **Twilio SMS service**, you have first of all to setup and buy the Twilio SMS service; once don that, you have to specify the last three parameters in this section.

**Email suffix when sending SMS** - used in case of an external SMS email gateway: it represents the domain of the email service; for example, if you have a phone number like "3401234567", you email suffix can be "mycompany.com" and Platform will send an email message like "3401234567@mycompany.com" to the SMS gateway, which then sends the SMS message to the specified number \(the left part of the email address\).

**From SMS Phone Nr** - used in case of an external SMS email gateway: it represents the "from number" to use when sending SMS messages and it must be recognized by the SMS email gateway.

**Default International prefix for SMS** - used in case of SMS sent through the Twilio SMS service: it represents the international prefix number to include to the specified phone number, in case this one does not include also the international prefix number; for example, suppose you have defined here a default international prefix like "+39", if you pass forward a phone number like "+393401234567", this number does not change, but if you pass forward a phone number like "3401234567", this number will be replaced internally by Platform with "+393401234567" and passed to the Twilio SMS service.

**Twilio SMS Account SID** - used in case of SMS sent through the Twilio SMS service: it represents the username provided by your Twilio account that you have already had to setup.

**Twilio SMS Auth Token** - used in case of SMS sent through the Twilio SMS service: it represents the authorization token provided by your Twilio account that you have already had to setup.



### SSO

Use this section when you want to log on into your web application using an authentication system different from the default one, provided by Platform and named "4WS".

Platform supports multiple authentication mechanisms:

* **4WS** - the default authentication mechanism, based on the internal table named PRM01\_USERS
* **LDAP** - when a user is logging on, the authentication process is forwarded to an external LDAP server \(e.g. Microsoft Active Directory\), containing all user credentials \(username + password + additional user properties, like name, last name, email, etc.\); in such a scenario, it would be a good idea to activate also the LDAP synchronization feature provided by Platform, in order to retrieve all usernames \(not the passwords which are only maintained internally yo the LDAP server\) and additional properties and store them in Platform as well; in this way, you can inherit and access all additional properties and link these usernames to the authorization module provided by Platform \(i.e. what a user can do after a successful authentication process - permissions\)
* **GMail SSO** - the login page would include also the Google SSO dialog, composed of the Google email input field and password input field and the Login button: in case the user has already logged on Google suite, this login page would automatically recognize the login and by-pass it, by showing after a few seconds the Platform web app main page.
* _**Custom SSO server**_ - you can define a server-side javascript action which would be invoked behind the scenes by Platform when the user attempts to log-on: it is up to this action to figure out if the user is allowed to log on, by invoking external authentication system; this action receives in input the user credential typed by the user in the login page and can pass them forward to external system: finally the action be provide the outcome and even replace some input data with others \(e.g. change the username provided by the user and expressed as an email address to a totally different value for the username, provided by the external system\).

All these authentication mechanisms can be combined together, if needed, as an **authentication chain**, that is to say, the authentication process can try more than one mechanisms, combined in sequence, like a chain: for example "4WS + LDAP": try first to authenticate through the default auth mechanism and in case of failure try through the external LDAP server.

**Authentication chain \(opt. def. '4ws'\)** - this parameter is mandatory \(here or as global parameter\); it defines the authentication chain described above; allowed values are for example: 4WS, 4WS + LDAP, etc.

**Sync: Company,site couples to use when creating records \(opt. def. all\)** - this is an optional parameter; if specified, you have to define couples of company + site ids, where the company id is separated by the site id with a comma \(,\) and a couple with another with a ;

Example: 

```javascript
00888,100;00888,101;00889,100
```

Platform will use this parameter to auto-create user entries in the internal user table PRM01\_USERS, starting from the username provided by the external LDAP server: for each LDAP's username, Platform will duplicate this username for each company and site specified, in case of a multi-tenant web application.

If this parameter has not been specified, the default behavior would be to auto-create usernames for each combination of company and site ids.

**Sync: Logical delete of users before sync \(opt. def. false\)** - \(opt. – true or false\). If true delete the users from the current source before trying to write the new ones. Default: false. It is important to understand if the source list is full or incremental \(only new or updated users\): this depends on the sources settings. In the first case the deletion can be enabled, in the second case must be disabled.

**Sync: Fields to manage in 4WS users table \(opt.\)** - \(opt.\) semicolon \(;\) separated list of 4ws.Platform user object fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields. 

Default value: “pk.userCodeId;description;password;;”. 

Note: in the 4WS.Platform DB the user data is spread among different tables that PRM01\_USERS. For example the mail is in SUB01 other info are in PRM08. To fill this fileds with the value from the source, specify the table prefix before the field, for example: SUB01.EMail, SUB01.firstName, SUB01.lastName.

The possible values are: 

* userInitial: string. User initials 
* description: string. User description 
* password: string. User password 
* dateExpirationPassword: date. Password expiration date 
* locked: string Y/N. Locked account 
* lockDate: date. Locking date 
* erasable: string Y/N. If Y the user can be deleted by the sync process 
* initValidate: date. User validity starting date 
* endValidate: date.User validity ending date 
* isAdmin: string Y/N. The user is admin 
* SUB01.EMail: string. Email addres 
* SUB01.firstName: string. Names 
* SUB01.lastName: string. Surname 
* SUB01.sex: tipo string M/F/O. Gender 
* SUB01.address: string. Address 
* SUB01.zipCode: string. ZIP code 
* SUB01.city: string. City 
* SUB01.country: string. Country 
* SUB01.province: string. Province or state 
* SUB01.birthdate: date. Birth date 
* SUB01.telephone: string. Phone number 
* SUB01.mobile: string. Mobile number 
* PRM08.languageId: string. ISO2 language code \(i.e.: it, en, fr, de …\) 
* PRM08.userImageUrl: string. User image URL.

**Sync: Fields to manage in 4WS groups table \(opt.\)** - \(opt.\) semicolon \(;\) separated list of 4ws.Platform group object fields target of the data coming from the source. The fields must correspond to the source field, can be empty but they must be in the same quantity of the source fields. 

Default: “pk.roleId;dictionary.description” \(see Prm02Groups fields\)



### TENSOR FLOW

TensorFlow password

TensorFlow url



### UI

This section contains a set of properties which change the UI appearance of your web application. The correct values for these settings depend on the chosen theme, since a specific them has a different menu, topbar content, bottom bar, etc.

**Single Document Interface \(Y/N\) \(predef. N\) -** check this property only in case you want to create a single document interface, i.e. a very simple web application \(like a web site\), where there aren't multiple windows to show at the same time \(e.g. a list of data + a detail window for a selected row\); the SDI paradigm states that only only window is visible at a time and consequently only very basic application UIs can be created.

**Application icon** - a .ico public file to use as "favourite icon" for the web application \(i.e. showed by the browser on the URL bar\). If specified, this .ico file is loaded starting from the platform web context.

Example:

&lt;my app web context&gt;/images/favicon.ico

**Menu levels** - Platform supports a series of different menu types:

* popup menu anchored to the left side of the application, opened by clicking on the button on the top-left side \(the most modern menu\); there is also a variant of this menu, where the application functionalities are organized within this popup window in a hierarchical way, rather than a plain list\). This menu is good for applications having a large amount of application functionalities
* popup menu anchored to the top-right side of the application, opened by clicking on the corresponding button; application functionalities are organized in folders and subfolders, within this popup window. This menu is good for small applications, having a limited amount of application functionalities
* the application main area is filled with the menu, represented as a list of buttons and sub-folders
* a menubar organized in one or two levels \(the oldest menu\); in this menu, the application functionalities are organized in two levels: a first level bar where a set of menus are reported; when the end user click on one of them, the submenu items for the selected menu are reported in the second level menubar \(on the bottom on the first level menubar\).

This parameter defines the number of menu levels: it should be always set to 0 for all applications except for the ones having the oldest menu type \(menubar\), where it can be set to 1 or 2.

**Show window icon \(Y/N\)** - in case of old applications where windows are not tabs but internal windows, this checkbox allows to show an icon for each window \(defined through the Window detail in the App Designer\).

**Context help** - Platform supports a context help for the App Designer and for a web app.

In the App Designer is accessible by clicking on a label of an input field in any Designer's window.

In order to activate the context help, this parameter must be set to "Readonly": in this case, the end user can click on the link and see a tooltip explaining the meaning of the current field.

If you set it to "Edit" \(in your dev env\), these links on labels are clickable and editable: the dev user can click on the link and see/edit the tooltip explaining the meaning of the current field.

**Top bar height \(pixels\)** - the top bar is showed on the top part of a web application. This parameter allows to define its height. Default value: 60. The value to set strongly depends on the chosen theme.

**Enable menu file \(true/false\)** - checkbox used to show an additional menu items in menu-bars menus, named "File" and used to include default menu commands, like "Exit".

**Favourite icon suffix** - 

**Popup windows with closing button \(def. N\)** - checkbox used to define whether all windows showed in the application which are modal must include also a close button on the top right corner. It is recommended to select it.

**Menu tree width** - in case of a tree menu type \(an old menu type\), defines the menu window width

**Modal windows with closing button \(def. N\)** - 

**Enable menu filter \(true/false\)** - 

**Status bar height \(pixels\)** - the status bar is the bottom part of a web application. This parameter allows to define the bottom bar height.

**Use default icon for user profile when not found \(def. N\)** - checkbox used to define if a the default icon for the user profiles must be used if not defined in the CSS explicitelly. Otherwise the icon will not be showed at all.

**Order of Grid Export** - this text parameter allows to define which export formats are supported by the application, when clicking on the export button in a grid: a popup window is prompted where the end user can choose among the export formats supported. This parameter defines the formats list and the order in the combobox. Supported values are:

* XLS
* Extended XLS
* CSV;
* CSV,

The parameter value can contain any of these values, separated by the pipe symbol \|

**View asterisk on mandatory controls \(Y/N\) \(default N\)** - as default settings, all mandatory cells on a grid have a pink color background, if there is not content set yet, in order to highlight where there are cells to fill in before saving data; same for a form panel: all mandatory input controls not filled yet have a pink colored background. 

When this checkbox is selected, an alternative approach is used to highlight the mandatory controls: an asterisk \(\*\) is showed at the right of each label, for each mandatory input control. Consequently, this approach consumes more space horizontally in a window, since a \(\*\) text is also included for each mandatory control.

Moreover, a legend explaining the meaning of the \(\*\) is reported at the bottom of each panel and subpanel.

**Message for empty panel** \(mobile apps only\) - for a grid having no rows, the default behavior is to report on the bottom of the grid the number of rows fetched, in this case zero.

If this checkbox is selected, an additional message is also prompted to the user.

**First level menu height \(pixels\)** - to use only for web apps having two levels of menubars \("Menu level" parameter set to 2\), i.e. the application functionalities are organized in two levels: a first level bar where a set of menus are reported; when the end user click on one of them, the submenu items for the selected menu are reported in the second level menubar \(on the bottom on the first level menubar\).

This parameter defines the first level menubar height and should be always set to 0 for all applications not using two levels menubars.

**Second level menu height \(pixels\)** - 

**Grid in edit with double click \(YN\) \(default N\)** - 

**Show alert in menubar \(Y/N\)** - checkbox used to show an icon on the topbar, on the right. This icon highlights when an alert message is arriving for the current logged user \(generated on the server layer through the utils.sendAlertMessage method\). This is a clickable icon: when the user clicks on it, a popup menu is showed, reporting all incoming alert messages \(not read yet\).

**Hide icons in tabs menu \(Y/N\)** - checkbox used to show an icon on the tabs representing opened windows. The icon can be defined in the Window detail.

**Text filter by enter \(Y/N\) \(default N\)** - checkbox used to listen to ENTER pressure: when selected, the end user can move from an input field to the next one, not only using the TAB key but also using the ENTER key.

Note: usually the ENTER key should be used only for lookup  controls, where its pressure lead to the code validation for the text just typed in.

**Show short unique key** - checkbox used to show a more user friendly error message, in case of SQL errors on saving data due to a unique key violation on the database.

If selected, Platform does not show the error coming from the database, but a more user friendly message. You can customize this error message through the Translations functionality, by adding the custom entry:

common.a unique key has been violated

**Toolbar buttons expand \(Y/N\) \(default N\)** - 

**Loading order of the context css files** - "Default" to load all .css files found the app web context in the order they have been written in the file system; "Sort by name" to read them by name. The second option is safer, since it is always predictable and conflicting CSS class names would be read in the clear order.

**Read CSS context files only from css/css\_login folders** - checkbox used to limit the amount of .css files to read form the web public context of the application. As default behavior:

* in the login page, Platform scans and load on the UI all .css files found in the "css\_login" subfolder
* for the main page \(i.e. after a successful login\), Platform scans and load on the UI all .css files found in the whole public web context, except for the "css\_login" subfolder

If this checkbox is selected, for the main page \(i.e. after a successful login\), Platform scans and load on the UI only .css files found in the "css" subfolder.

**View asterisk on mandatory controls only when needed \(Y/N\) \(default N\)** - as default settings, all mandatory cells on a grid have a pink color background, if there is not content set yet, in order to highlight where there are cells to fill in before saving data; same for a form panel: all mandatory input controls not filled yet have a pink colored background. 

When the checkbox "View asterisk on mandatory controls**"** \(described above\) is selected and ALSO this checkbox is selected, a legend explaining a the meaning of the \(\*\) is reported at the bottom of each panel and ONLY for the subpanels containing at least one mandatory controls. Consequently, the window containing subpanels would consume lesser space in height, since the number of legends to show is minimized.

**Label position of Designer functionality** - for each input field defined in a form panel, editor panel and filter panel, a label is also included, explaining the meaning of the field.

This label can be showed either on the left of the input field or on top of it.

This parameter allows to define the position of the label: Top or Left \(default\).



### USERS

**Supported user languages Component Id**  - optional parameters, helpful for a multitenancy application, where the supported languages could vary according to the tenant. 

When not settings this parameter, the languages defined through the App Designer are valid for all applications defined in the Platform installation, through the Languages functionality. 

When this parameter is set, the "Language" combobox available in the user detail would show not any more the whole list of languages defined through the Languages functionality, but a subset of it, whose sublist can be filtered according to application logic depending on the company id \(tenant\).

In any case, if this parameter is filled in, it must be the id of a server-side javascript business component, whose JSON result must be the same required by the "Language" combobox in the user detail window.

Example:

```javascript
utils.setDecodeField("pk.languageId","LANGUAGE_ID");

var langIdsIn = "..."; // my custom app logic
var json = utils.getPartialResult(
    "SELECT * FROM SYS11_LANGUAGES WHERE COMPANY_ID= ? AND STATUS='E' and LANGUAGE_ID IN ("+langIdsIn+")",
    null, 
    false,true,
    [userInfo.companyId]
);
var res = JSON.parse(json);
for(var i=0;i<res.valueObjectList.length;i++) {
    res.valueObjectList[i].pk = {
        companyId: res.valueObjectList[i].companyId,
        siteId: res.valueObjectList[i].siteId,
        languageId: res.valueObjectList[i].languageId
    };
}

utils.setReturnValue(JSON.stringify(res));
```

**Action id \(JSServer\) to use after change password** - this optional parameter can be used to specify a server-side javascript action which will be invoked by Platform, each time a user changes its password. It can be used as a callback for such event and execute some custom logic.

Example:

```javascript
// in input the predefined "vo" is prefilled with:
// { 
//   companyId: "...",
//   siteId: ...,
//   username: "...",
//   oldPassword: "...",
//   newPassword: "..."
// }

// after executing some custom logic, it is also possible to block the password change, 
// by getting back a JSON containg a success: false:
utils.setReturnValue(JSON.stringify({
  success: false,
  message: "the reason..."
}));
```

**Action Id \(server-side js\) to be performed after insert/update/delete a user** -  this optional parameter can be used to specify a server-side javascript action id which will be invoked by Platform, each time a user is added/modified or deleted. It can be used as a callback for such event and execute some custom logic.

According to the operation, the input provided to the javascript action is different.

In case of insert:

```javascript
reqParams = {
  operationType: "insert"
}

vo = ... // the user detail content

headers = ... // the ones provided by the browser
```

In case of update:

```javascript
reqParams = {
  operationType: "update"
}

vo = ... // the user detail content

headers = ... // the ones provided by the browser
```

In case of deletes:

```javascript
reqParams = {
  operationType: "delete"
}

vo = { valueObjectList: [... ] } // the list of users to delete

headers = ... // the ones provided by the browser
```

**Flag used to hide the warning message when saving user roles \(def. N\)** - checkbox used to hide the confirm message appearing when the user is saving a user detail

**Action Id \(server-side js\) to take before you insert/update/delete a user** - this optional parameter can be used to specify a server-side javascript action id which will be invoked by Platform, each time a user is about to insert/update or delete users. It can be used as a callback for such event and execute some custom logic, in order to prevent the change in the database and interrupt the operation.

According to the operation, the input provided to the javascript action is different.

In case of insert:

```javascript
reqParams = {
  operationType: "insert"
}

vo = ... // the user detail content

headers = ... // the ones provided by the browser

// after executing some custom logic, it is also possible to block the operation, 
// by getting back a JSON containg a success: false:
utils.setReturnValue(JSON.stringify({
  success: false,
  message: "the reason..."
}));
```

In case of update:

```javascript
reqParams = {
  operationType: "update"
}

vo = ... // the user detail content

headers = ... // the ones provided by the browser

// after executing some custom logic, it is also possible to block the operation, 
// by getting back a JSON containg a success: false:
utils.setReturnValue(JSON.stringify({
  success: false,
  message: "the reason..."
}));
```

In case of deletes:

```javascript
reqParams = {
  operationType: "delete"
}

vo = { valueObjectList: [... ] } // the list of users to delete

headers = ... // the ones provided by the browser

// after executing some custom logic, it is also possible to block the operation, 
// by getting back a JSON containg a success: false:
utils.setReturnValue(JSON.stringify({
  success: false,
  message: "the reason..."
}));
```

**Action id \(JSServer\) to use after application user logout** - this optional parameter can be used to specify a server-side javascript action id which will be invoked by Platform, each time a user has logged out from the web application.

Available inputs are:

```javascript
userInfo = { ... } // user info

headers = ... // the ones provided by the browser
```



### VOICE

Activate voice synthesize \(Y/N, def. N\)

Start voice command \(e.g. platform\)



### WHATSAPP

**Secret key** - required as well as "account id": the value is defined in the Twilio Whatsapp Admin Console

**Phone number used as sender** - the phone number to use when sending email; it is required and to define first in the Twilio Whatsapp Admin Console

**Action id for Whatsapp callback** - optional value: if set, it is a server-side action, defined as PUBLIC web service \(i.e. no credentials are required when invoking it\); this field is needed only in case you want not only send Whatsapp messages but also get feedbacks, like "message sent" or "message read": this is the callback ws which receives these events from the Whatsapp service.

**Account id** - required as well as "secret key": the value is defined in the Twilio Whatsapp Admin Console

### REPORT DOCX

**\(v6.0.2\) Directory id for report Docx** - you can specify the directory to save docx templates to generate reports. If not specified they are saved in the context of the application.





## 

