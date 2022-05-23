# Global parameters

Global parameters are accessible starting from the menu **Administration** -> **Global Parameters**. Once opened it, a list of parameters can be defined.\
Some parameters are global only, i.e. applied to all applications defined in the environment, others can be redefined at application level; some others can be defined at application level only.\
The followings are global parameters, grouped per topic:

###

### 4WS.PLATFORM

**Database version** - readonly parameter, automatically set by Platform when its service is started; it reports the current version of the database/application. ****&#x20;

**Index page file** - optional parameter used to define which is the main page for applications.

**Speed up metadata import (def. N)** - checkbox used to increase the metadata import process, by speeding up the writing operations on database.

**Offset of Device Application activation key path** - parameter used by the offline module

**Base Mobile Sync Path** - optional parameter; it represents a base path in the file system of the Platform server, used when creating a new mobile app: it is used as a default base path for the mobile app for all mobile sync content.

**Force all names to lowercase for headers in HTTP requests (def. Y)** - header names are passed forward in lowercase by many web servers and cloud services, so it would be better to select this checkbox.

**Starting web page** - URL representing the base URL of this Platform installation; it is recommended to set it up, since it is used widely by Platform, for example when sending emails containing references to this server.

Example:&#x20;

https://yourhouse/platform/

**Do not allow to set server variables from the client side** - checkbox used to block any attempt to change server-side variables from the UI (not a safe approach).

**Max nr. of actions in history** - it is strongly recommended to set it, e.g. to 10; it is used behind the scenes by Platform every time a dev saves the action content: the previous version of the action content is saved, so it is possible for the dev to compare previous version and if needed, to restore some parts.

**Sinesy Email Address** - email address used as default "from address" every time an email is sent.

**Database upgrade in progress** - read only value, used internally by Platform with a cluster environment, when an upgrade is in progress (when starting up the Platform service); used to avoid database locked due to multiple nodes started at the same time: only the first setting this flag is granted to continue the upgrade.

**Web Designer activation key path** - optional parameter to use in case no activation key has been uploaded at application level; this is an absolute path in the file system of the Platform server to a folder containing the activation keys.

**Duplicate data per company (Y/N def. Y)** - check to use with applications working with multiple tenants: if selected, every time a function is created, it is automatically duplicated for each company id.

**Allow the use of additional filters (low security)** - it is strongly recommended NOT to select this checkbox: if you select it, you can pass forward from the UI to the server layer additional SQL conditions which could represent a security leak (SQL injection).

**Create EntityManager for additional sources (list of packages)** - ****&#x20;

**Do not allow to pass a SQL filter on panel loading** - checkbox used to block any additional condition when invoking the standard web service getlist, used to fetch a list of records (for a grid or a selector). If not checked, it is allowed to pass a SQL fragment to the base SQL query executed on the server side, which would represent a SQL injection risk.

It is strongly recommended to select it.

If you have SQL based business components which work with additional SQL filters, you can fix this situation using the following steps:

* replace the SQL based business component with a JS business component
* copy the same base SQL query in the new component, using utils.getPartialResult
* embed within the new component any custom logic thast previously you defined using addional SQL filters.

**Take into account the difference between UTC and GMT for datetime** - checkbox used to change the date+time value to show in grids/forms, by taking into account the time zone difference between the client and the server.

It is strongly recommended to select it.

**Take into account the difference between UTC and GMT for date** - checkbox used to change the date value to show in grids/forms, by taking into account the time zone difference between the client and the server.

It is strongly recommended to select it.

**Do not set fetch size on SQL queries (def. N)** - as default behavior, all SQL queries are limited in size by a number of records equal to the max length specified by a grid + 1. It is strongly recommended not to select this checkbox, otherwise the JDBC driver could fetch a very long result set from the database server and cache it internally: such arbitrary behavior can easily due to  out of memory errors and slow query executions. You can select this checkbox in case you have weird behaviors in the number of rows returned by a business component, such as when you are not enquiring a database table but something else, like a stored function.

**(v5.3.2) Use minified js files (def. N)** - the applications uses minified javascript and css files to reduce the size of running files

**Fast metadata loading** - if checked, it speeds up the application reloading process, therefore, it is helpful in a development environment, where metadata is always changing, due to the dev team working on the application all the time. More precisely, when selected, it avoids to reload changes on server-side and client-side actions, which are the most commonly changed artifacts.&#x20;

Pay attention that in case of changes in a client-side js action, you have still to reload the web application on your browser, since the code has been already loaded, but the web app reloading will be faster, since no metadata loading process is needed.



### ACTIVITI

These parameters are also defined at application level.

**Tomcat Path of Activiti** - the absolute path to set, related to the installation of Activiti within a Tomcat.

Example:&#x20;

/opt/tomcat-activiti/

**Base Rest URL of Activiti** -  base URL of Activiti; it can be an internal URL not a public URL.

Example:

[http://localhost:8280](http://localhost:8280)

**Base Designer URL of Activiti** - base URL of Activiti, used to access Activiti Explorer (i.e. the BPM designer); it must be a public URL.

Example:

http://host/



### ALERT

Parameters related to alert messages in case of a cluster based Platform installation (multiple servers)

Pre-requisite: the WEB-INF/web.xml file must have been set with "cluster" tag value set to "true"

**Messages messages main node URL** - if set, this public URL will be used to send all notification events; this URL represents the public URL for the main fixed node; use this setting ONLY when you have a cluster where there is a fixed main node; i this parameter is filled, it is&#x20;

**Port for the messages main node (opt.)** - this parameter must be filled together with the next one: it represents the internal Tomcat port where the main current node is listen for requests

**Protocol for the messages main node (opt.)** - this parameter must be filled together with the previous one: it represents the HTTP protocol to use (http vs https) to use when communicating with the internal Tomcat where the main current node is listen for requests



### **ALFRESCO**&#x20;

parameters related to the ECM module

* Admin Password when connecting to Alfresco Server
* Admin Username when connecting to Alfresco Server
* URL when connecting to Alfresco Server
* sync user in Alfresco
* sync roles in Alfresco
* sync user roles in Alfresco

### ****

### **APP ANALYSIS**&#x20;

Parameters related to the tool used to perform an assessment of the app

**Enable application analysis every X hours (def. disable)** - in order to start the app analysis, you have to fill in this parameter: this number represents the hours to wait before the next analysis. A good value can be 4 o 8 hours.

**Email used to send notifications after an app analysis** - when the app analysis has started (through the previous parameter), Platform can send a notification email with all events analized which overpass the triggers set on the app analysis definition window. This is the email address where the email messages will be sent. Multiple email addresses are supported: use the comma (,) symbol to separate each other.

**Destination Phone Nr. when sending SMSs after an app analysis** - when the app analysis has started (through the first parameter), Platform can send a notification SMS message with all events analized which overpass the triggers set on the app analysis definition window. You have also to correctly set Twilio parameters for SMS (see SMS section). This is the phone number where the SMS messages will be sent.

**Subject to use in SMS/email after an app analysis** - in case of notification by email, this parameter must be filled in as well.

### ****

### **DOCX CONVERSION**&#x20;

parameters related to the services which allow to convert documents to the PDF format

### ****

### **EXPORT**

Parameters related to the xls export module.

Platform supports a variety of different export formats:

1. csv with ; or , as separator
2. xls
3. xlsx
4. xls with codes instead of decoded descriptions

In any case, it is possible to use different libraries to execute the export. Not all libraries have the same capability:

* HSSF library: it is the default settings and consumes a lot of memory during the export process, so it is not recommended to use it for very large exports (millions of cells)
* LibreOffice Portable, a free application to "install" in the Platform server

**Export to xlsx using HSSF library (Y/N def. N)** - checkbox used to choose which library to use (see above)

**Max number of exportable rows in grid** - this is a very important parameter; it is strongly recommended not to set a too high value (no more than 100000), otherwise the memory consumption of the server could lead to memory errors and instabilities.&#x20;

**Max. nr. of concurrent exports before enqueuing them (def. 1)** - it is recommended to set this parameter, in this way the memory consumption of the server will be under control.

**Path LibreOffice for export** - to fill in only in case the checkbox "Export to xlsx using HSSF library (Y/N def. N)".

### ****

### **FILE UPLOAD**&#x20;

Parameters used to manage the file upload

**File Storage (FILE\_SYSTEM or GCS or GDRIVE; def. FILE\_SYSTEM) File System** - this parameter defines the media to use when uploading files, among the 3 alternative medias: Platform server file system, Google Cloud Storage, Google Drive.

**Default path for directories** - an absolute path to use as base dir for all uploaded files (for all defined directories), in case of upload based on file system.

**Google Project Id** - in case of file upload saved on Google Cloud Storage, it is required to specify here the Google Cloud Project Id used by the GCS service.

**Create subfolders for company and site (YN def. Y)** - in case of a multi-tenancy app, it is possible to auto-create subfolders for each company id / site id, so that each tenant can access and use his own files.

**Loading directory on startup** -&#x20;

**(opt.) Autodefine file name for uploaded files** - in order to ensure file names uniqueness, it is a good idea to select this checkbox: in this way, all uploaded files are automatically renamed to a unique name and cannot in any way override existing files.

### ****

### **GOOGLE**&#x20;

Parameters used to integrate the application with the Google Cloud Platform and the Google Domain (GSuite)

**Google Datastore id** **-** in case of app connected to the Google Datastore NoSQL database, this is the Google Cloud Project Id (mandatory)

**Namespace list when exporting towards Platform for GA (, separated)** - in case of app connected to the Google Datastore NoSQL database, this is the namespace to use. If not specified, the default namespace will be used.

**Google Service Account Key (p12 key Base64 encoded)** - in case of apps connected to any Google Cloud service (including Google Datastore), this is the service account key, converted in text (p12 format, base64) generated using the Google Cloud Console

**Service Account Email** - in case of apps connected to any Google Cloud service (including Google Datastore), this is the service account email generated using the Google Cloud Console; together with the previous parameter, they represent the GCP credentials, essential to access to the GCP services.

**Apps domain admin user for Google Service Account** - in case of apps connected to any Google GSuite service (now Google Workspace), this is the service account email generated using the Google GSuite Console

**Google SSO** - **Client id for web application** -&#x20;

**Google SSO** - **Client secret for web application** -&#x20;

**Google SSO** - **Format to extract username from email** -&#x20;

**Google Sync** - **Apps domain to use for synchronization** - the Google Apps domain name (for example mygoogleappsdomain.com) from which users and groups must be read. In case of multidomain Google Apps, only the objects of this domain are read. This parameter takes precedence over the next one, customer id.  &#x20;

**Google Sync** - **Apps customer id used for sync** - in case of multidomain Google Apps, specify the customer id of the Google Apps installation.

**Google Sync** - **User query for synchronization** -  (opt) a filter query for users list, as specified in the documentation: [https://developers.google.com/admin-sdk/directory/v1/reference/users/list](https://developers.google.com/admin-sdk/directory/v1/reference/users/list). For example: eMail:a\* to extract only users whose e-mail address starts with “a”.  &#x20;

**Google Sync** - **Format to extract username from email for sync** - (opt) specify this to convert the user email in 4WS.Platform user id. It works like the similar parameter user for SSO. In case of multidomain pay attention that only one parameter can be specified. Default value is {u}.&#x20;

**Google Sync** - **Fields extracted from user accounts** - user fields that will be mapped in the destination fields.&#x20;

The default value is&#x20;

```
primaryEmail;description;;;
```

The available fields name are specified in Google API documentation ([https://developers.google.com/admin-sdk/directory/v1/reference/users#resource](https://developers.google.com/admin-sdk/directory/v1/reference/users#resource).&#x20;

Use the first level attributes, nested attributes are not supported) and the following custom values: description, name, surname. &#x20;

**Google Sync** -  **Type of fields extracted from user accounts for sync** - user field types used to extract the date.&#x20;

The default value is&#x20;

```
UserFormatType;;;;
```

where the first type indicates that the first field is the user name, in string format. The default are string fields.&#x20;

**Google Sync** - **Fields extracted from group information for sync** - group fields that will be mapped in the destination fields.&#x20;

The default value is&#x20;

```
name;description
```

**Google Sync** - **Type of fields extracted from group information for sync** - user field types used to extract the date.&#x20;

The default value is&#x20;

```
;
```

indicating two string fields.

**Google Sync** - **Sync: company, site to use when creating records from Google** -&#x20;



****

### **LDAP**&#x20;

parameters used to integrate the app with an LDAP server, like MS Active Directory

* Autocreate user from LDAP
* Autoupdate user from LDAP
* Autoassign current role to new LDAP user
* checking enabled
* port
* server
* account auth format
* Sync: company, site to use when creating records from LDAP
* LDAP synchronization
* Password to use when connecting to LDAP
* Username to use when connecting to LDAP
* Base LDAP path when searching for users
* (optional) Users LDAP filter
* (optional) fields to manage in LDAP users
* (optional) field types to manage in LDAP users
* (optional) LDAP attribute for user id
* Base LDAP path when searching from groups
* (optional) Groups LDAP filter
* (optional) fields to manage in LDAP groups
* (optional) field types to manage in LDAP groups
* (optional) LDAP attribute for group id

### ****

### LOGS

**Max days to log** - this parameter is related to the Table Log, i.e. log saved to CON60\_LOGS table.

It is essential to put a limit to the log events to save here. Please always set it, for example to 60 (days).

**If  only "Max days to log" is filled out, then this setting will be applied to all log types**. Consequently, if you want to set a specific limit for a specific log type, you have NOT to define "Max days to log" as a global parameter (let it empty), but use **"Max days to log per Type" instead, available as an application parameter (**[**https://4wsplatform.gitbook.io/user-guide/setting-up-the-environment/3-1-18-2-application-parameters#logs**](https://4wsplatform.gitbook.io/user-guide/setting-up-the-environment/3-1-18-2-application-parameters#logs)**)**.

### LOGIN

**Enable Two Factor authentication for web apps** (since 6.0.2) - when activated, the two factor authentication is required in the interpreted the web apps: the login page will show not only username and password fields, but also the OTP input field where typing the one-time-password generated through a mobile app.

Once enabled this feature, the login page would ask ALL users to provide the additional OTP when logging on, through the new _OTP input field_ available in that page.&#x20;

_Failed attempts when typing the OTP count for invalid attempts_ as well as for the invalid password and would lead to lock the account after reaching the maximum attempts.

The first time you logon in the web app (OTP field with "unset" value...), a QRCode is displayed and must be captured through the camera of the smartphone, opened starting from either Google Authenticator or Microsoft Authenticator or Twilio Authy.

Once captured the QRCode in one of these apps, the user has to type the OTP code displayed in the mobile app and press the "Login" button.&#x20;

Similarly, after the first time, the user can access to the OTP code in the mobile app, read it and type in the OTP input field of the web app login page.

As reported above, the user can install in his own smartphone any of these free apps:&#x20;

* _Google Authenticator_ - it is the easiest of the three: it can protect your private keys through your smartphone auth mechanism (e.g. Face ID) but only in the iOS version
* _Microsoft Authenticator_ - as for the previous one, it can protect your private keys through your smartphone auth mechanism (e.g. Face ID, fingerprint reader) and it can also backup the user private keys in the cloud (backup), but only if the user owns a Microsoft account.
* _Twilio Authy_ - as for the others, it can protect the user private keys through his smartphone auth mechanism (e.g. Face ID, fingerprint reader) and it can also backup the private keys in the cloud, by creating a free account in the Authy cloud. It supports also multiple devices.

It is recommended to use the last one, since it is the most complete.



**Enable Two Factor authentication for App Designer** (since 6.0.2) - when activated, the two factor authentication is required to developers to access the App Designer: the login page will show not only username and password fields, but also the OTP input field where typing the one-time-password generated through a mobile app.

Once enabled this feature, the App Designer login page would ask ALL developers to provide the additional OTP when logging on, through the new _OTP input field_ available in that page.&#x20;

_Failed attempts when typing the OTP count for invalid attempts_ as well as for the invalid password and would lead to lock the account after reaching the maximum attempts.

The first time the developer logon in the App Designer (OTP field with "unset" value...), a QRCode is displayed and must be captured through the camera of his smartphone, opened starting from either Google Authenticator or Microsoft Authenticator or Twilio Authy.

Once captured the QRCode in one of these apps, the user has to type the OTP code displayed in the mobile app and press the "Login" button.&#x20;

Similarly, after the first time, the user can access to the OTP code in the mobile app, read it and type in the OTP input field of the App Designer login page.

As reported above, the user can install in his own smartphone any of these free apps:&#x20;

* _Google Authenticator_ - it is the easiest of the three: it can protect your private keys through your smartphone auth mechanism (e.g. Face ID)
* _Microsoft Authenticator_ - as for the previous one, it can protect your private keys through your smartphone auth mechanism (e.g. Face ID, fingerprint reader) and it can also backup the user private keys in the cloud (backup), but only if the user owns a Microsoft account.
* _Twilio Authy_ - as for the others, it can protect the user private keys through his smartphone auth mechanism (e.g. Face ID, fingerprint reader) and it can also backup the private keys in the cloud, by creating a free account in the Authy cloud. It supports also multiple devices.

It is recommended to use the last one, since it is the most complete.

**Disable RTK sensitive parameters after login (def. N)** - flag used to disable sensitive parameters to load in the main page after the login step.

**Enabled users** - list of users, separated by a comma, who can access the web app; helpful to limit temporarely the logon to a restricted set of users, for example when deploying a new app version and need sometime to test it.

**Show combos for Company and Site (YN)** - flag used to show either a combo or an input field for company and site id fields.

**Server-side action before login** - you can optionally specify the id for a server-side js action which will be invoked just after a successful login, in order to carry out an additional checking and optionally interrupt the login (e.g. after checking the browser IP address or the access time).

The action can interrupt the logon through the method:

```
utils.setReturnValue({ 
  success: false, 
  message: "Message to show" 
  });
```

**Login label in controls** - set the labels for the login controls

**Access Unavailable message** - message to show in the login page, when the login has been temporarely suspended.

**Translate login labels with browser language** - flag used to automatically translate labels in the login page, according to the browser language.



### MAIL

The same parameters can also be redefined at application level.

**SMTP host when sending email** - the host name of the SMTP server used to send email messages; this parameter is mandatory; examples: smtp.mandrillapp.com or smtp.gmail.com

**SMTP port when sending email (opt.)** - the port used by the SMTP server to accept email messages to send; if not specified, the default port 25 is used; bear in mind that you cannot use the default port 25 if your Platform server has been installed in the Google Cloud Platform, since this port is blocked in the GCP. Moreover, the port also depends on the protocol used: smtp or smtps (SMTP over SSL).

**SMTP username when sending email (opt.)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**SMTP password when sending email (opt.)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**Use TLS when sending email: E/F (opt.)** - allowed values are E or F, i.e. enabled or forced and it depends on the SMTP server settings: check it out with the administrator of your SMTP server.

**Email Debug** - enable the debug of messages sent/received



****

### **MOBILE**&#x20;

Parameters used to integrate a mobile app with Firebase notification system and other settings.

**Google key for autocomplete place in iOS** - the google key defined through the Google Cloud Console to use the Google autocomplete place API within a mobile app for iOS.

**Google key for autocomplete place in Android** - he google key defined through the Google Cloud Console to use the Google autocomplete place API within a mobile app for Android.



### MONITOR

This section contains settings related to the "monitored services" module of Platform, i.e. the layer intercepting the server-side js action execution, when invoked by the web layer (web services), when invoked by the scheduled (scheduled processes) or when executed by the queue manager (enqueued actions). In all cases, these services are monitored and their execution traced.&#x20;

**Email used to send a message, in case of problems on services execution** - this is a mandatory parameter if you have monitored services configured to send notification emails in case of errors during the execution.

**Remote Platform URL n.1...10, used to retrieve log for the monitoring feature** - these 10 parameters can be used to connect the current Platform installation to up to 10 other remote installations, each containing monitored services. Here you have to define the remote URL to Platform installations invoked automatically to retrieve from these remote installations all monitored log and gather it in a unique repository, the current one.&#x20;

For more details see:

[https://4wsplatform.gitbook.io/user-guide/modules/ee10-1-log-and-analysis/service-monitoring/remote-platform-servers](https://4wsplatform.gitbook.io/user-guide/modules/ee10-1-log-and-analysis/service-monitoring/remote-platform-servers)

**Wait time before import log (hrs)** - a number, expressed in hours, related to the amount of time to wait before automatically retrieve all collected monitored log from the remote Platform installations. This parameter work along with the previous ones.

**Email subject to notify** - the email subject to use when sending notification emails.

****\
**Company id list to replace (e.g. 00000=A0000,00001=A0001)** - Fill in this parameter only in the questionable scenario where you are retrieving data from a remote application where data has been stored with a company id different from the one you are using in the current server and you want to match data of the two environments. In such a case, you can replace the company id value coming from the remote data and replace it with the one you specify through this parameter. By and large, you can specify a list of replacements (a list of company ids to replace and the new values).



### ****

### **PASSWORD**&#x20;

Parameters used to define the password policy.

**Password regular expression Password: regular expression explanation** - you can define a regular expression to respect when defining the passwords in the user detail window or when changing password on the login page.&#x20;

Example:

```
^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@$!%*?&])[A-Za-z\\d@$!%*?&]{8,}$
```

which means

* matches a string of 8 or more characters;
* that contains at least one digit (d is shorthand for \[0-9]);
* at least one lowercase character and
* at least one special character and
* at least one uppercase character.

**Password: number of days to use for the password expiration**&#x20;

**Password: number of erroneous login attempts** - when reached this number for consecutive failed authentications with the same username, the account will be locked. To unlock it, an admin must access the user detail and unlock it.

**Encrypt all passwords (Y/N)** - check used to force all passwords defined in PRM01\_USERS to be encrypted. The already existing records with plain passwords will be updated and the PASSWORD field will be a value converted to the encrypted text.

When unselecting this checkbox, all passwords in PRM01\_USERS will be converted to their plain version.

**Number of memorized passwords** - when a password expires, the user if forced to change it and his next access; Platform will not allow the user to type a new password already defined in the past: this parameter defines how many old passwords will be maintained behind the scene and checked to avoid their reuse.

**Send only encrypted passwords to the UI (def. N)** - checkbox used to transfer the user list objects and user detail object with the attribute password encrypted, so that it is not possible from the browser inspector to figure out the value of the password by looking at the network layer.

**EMail Template id for resetting password (example: EN=XXX,IT=XXX or only id for all)** - a list of template ids, for each language, used when sending an email to the end user who asked for changing password because he forgot his current password.



### **PERMISSIONS**&#x20;

Parameters used to define the authentication process

**Show site in users and user roles (Y/N)** - checkbox used to define whether the site id column/control must be showed in the users list and in the user detail window. As a default setting, this information is not visible.&#x20;

You should check this parameter when you have applications working with multiple site ids.

**Show role id (Y/N)** - checkbox used to define whether the role id column/control must be showed int he users list and in the user detail window. As a default setting, this information is not visible and consequently the role id is an auto-generated number reckoned by Platform behind the scenes.&#x20;

You should check this parameter only in case you want to be free to define the role id and not let Platform to generate it.

**Show/edit site in user detail (Y/N)** - checkbox used to define whether the site id control must be showed and be editable in the user detail window. As a default setting, this information is not visible and consequently the site id to use when inserting records is always the one owned by the current logged user.&#x20;

You should check this parameter only in case you want to be free to define the site id and not let Platform to generate it, i.e. when you have applications working with multiple site ids.

**Login controls to hide** - comma separated list of input fields in the login pane to hide. For example in a Platform installation where there is one only tenant (one only company id) or there is only one site id, it is useless to force the end user to specify them each time he logs on and they can be hidden and pre-filled.&#x20;

This parameter allows not only to define the list of input fields to hide but also the value to preset for them.

Example:

exit,companyId=00000,siteId=100

The example above would hide the exit button, the company id input field and preset it with a value of 00000, hide the site id input field and preset it with a value of 100.

Allowed input fields that can be hidden:

* companyId
* siteId
* language
* exit

**Check function Ids when reading data (Y/N def. N)**

**Automatically create users after successful authentication** - checkbox to select to auto-create a user when logging on (e.g. when the authentication is managed externally by an LDAP server).

**Update user from external authentication source (Y/N)** - checkbox to select in order to auto-update the user detail starting from data coming from external authentication servers (e.g. LDAP); if not selected, users are imported from external system but their data are not updated on time.

**Show only enabled roles** - used in the user detail window: if this checkbox is selected, the list of roles to show is filtered by the roles already owned by the current user; if not selected, all users can see all defined roles at application level, but can only select in the grid (in edit mode) the ones owned by the current user.

**Autoassign roles to new user (';' separated list)** - in case a user is auto-created when logging on (e.g. when the authentication is managed externally by an LDAP server), no roles have been assigned to him yet and consequently, it would not be possible for him to access the application, since two requirements must be fulfilled: a correct authentication + at least one role assigned to the user.

If this checkbox is selected, a user not having roles assigned yet, would inherit automatically the role (or list of roles separated by a comma) specified through this parameter and consequently he can access successfully the application.

**Default value for login controls** - ?

### ****

### **REDIS**&#x20;

parameters used to manage the integration with a shared cache for user sessions, based on Redis

**Server host name** - required in case of a fixed Redis server

**Server host port** - required in case of a fixed Redis server

**Instance name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the name used to identify the cache name in the Redis server

**Region name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the region name where the Redis instance will be created in the Google Cloud project

**Rest command to create an instance**  - in case of auto creation/destroy of the Google service based on Redis, this is an optional value, expressed in JSON format, related to the BODY content to send to GPC to create the instance

**Interval when Redis is not working** - in case of auto creation/destroy of the Google service based on Redis, this optional value represents the interval \[0-24] expressed with hours, where the service is not operating

**VPC name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the VPN name used by Redis and by the Compute Engine instances where Platform is running

### ****

### **SCHEDULER**&#x20;

Parameters used by the scheduler module

**"From email address" when sending email from Scheduler** - email address used by Platform when sending notification emails for a terminated scheduled process, if the dev has configured a notification at process level. This address will be used as the from address in the email messages.

**Force the main node for scheduled processes to be fixed (Y or N def. N)** - in case of a cluster of nodes where one is dedicated to the batch execution (scheduled processes and enqueued actions), this checkbox must be selected; moreover, the next parameter must be set as well.

**SCHEDULER\_IP** - the local IP address of the batch node, i.e. the node to use as "main node".



****

### **UI**&#x20;

Parameters used by the UI

**MESSAGES\_IP** - optional parameter, to set in case of a cluster having a main node used as the batch server; in such a scenario, set here the local IP address of the batch server

**MESSAGES\_PWD** - read only parameter, do not change it

**Order of Grid Export** - this text parameter allows to define which export formats are supported by the application, when clicking on the export button in a grid: a popup window is prompted where the end user can choose among the export formats supported. This parameter defines the formats list and the order in the combobox. Supported values are:

* XLS
* Extended XLS
* CSV;
* CSV,

The parameter value can contain any of these values, separated by the pipe symbol |

**View asterisk on mandatory controls (Y/N) (default N)** - as default settings, all mandatory cells on a grid have a pink color background, if there is not content set yet, in order to highlight where there are cells to fill in before saving data; same for a form panel: all mandatory input controls not filled yet have a pink colored background.&#x20;

When this checkbox is selected, an alternative approach is used to highlight the mandatory controls: an asterisk (\*) is showed at the right of each label, for each mandatory input control. Consequently, this approach consumes more space horizontally in a window, since a (\*) text is also included for each mandatory control.

Moreover, a legend explaining the meaning of the (\*) is reported at the bottom of each panel and subpanel.

**Hide Platform logo (Y/N)** -&#x20;

**Grid in edit with double click (YN) (default N)** - if this checkbox is selected, a grid can switch to edit mode not only by pressing the edit button but also with a double click on a cell.

**Loading order of the context css files** - "Default" to load all .css files found the app web context in the order they have been written in the file system; "Sort by name" to read them by name. The second option is safer, since it is always predictable and conflicting CSS class names would be read in the clear order.

**View asterisk on mandatory controls only when needed (Y/N) (default N)** - - as default settings, all mandatory cells on a grid have a pink color background, if there is not content set yet, in order to highlight where there are cells to fill in before saving data; same for a form panel: all mandatory input controls not filled yet have a pink colored background.&#x20;

When the checkbox "View asterisk on mandatory controls**"** (described above) is selected and ALSO this checkbox is selected, a legend explaining a the meaning of the (\*) is reported at the bottom of each panel and ONLY for the subpanels containing at least one mandatory controls. Consequently, the window containing subpanels would consume lesser space in height, since the number of legends to show is minimized.

### ****

### &#x20;

