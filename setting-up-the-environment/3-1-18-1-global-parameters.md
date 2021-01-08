# Global parameters

Global parameters are accessible starting from the menu **Administration** -&gt; **Global Parameters**. Once opened it, a list of parameters can be defined.  
Some parameters are global only, i.e. applied to all applications defined in the environment, others can be redefined at application level; some others can be defined at application level only.  
The followings are global parameters, grouped per topic:

### 

### 4WS.PLATFORM

**Database version** - readonly parameter, automatically set by Platform when its service is started; it reports the current version of the database/application. ****

**Index page file** - optional parameter used to define which is the main page for applications.

**Speed up metadata import \(def. N\)**  - checkbox used to increase the metadata import process, by speeding up the writing operations on database.

**Offset of Device Application activation key path** - parameter used by the offline module

**Base Mobile Sync Path**  - optional parameter; it represents a base path in the file system of the Platform server, used when creating a new mobile app: it is used as a default base path for the mobile app for all mobile sync content.

**Force all names to lowercase for headers in HTTP requests \(def. Y\)** - header names are passed forward in lowercase by many web servers and cloud services, so it would be better to select this checkbox.

**Starting web page** - URL representing the base URL of this Platform installation; it is recommended to set it up, since it is used widely by Platform, for example when sending emails containing references to this server.

Example: 

https://yourhouse/platform/

**Do not allow to set server variables from the client side** - checkbox used to block any attempt to change server-side variables from the UI \(not a safe approach\).

**Max nr. of actions in history** - it is strongly recommended to set it, e.g. to 10; it is used behind the scenes by Platform every time a dev saves the action content: the previous version of the action content is saved, so it is possible for the dev to compare previous version and if needed, to restore some parts.

**Sinesy Email Address** - email address used as default "from address" every time an email is sent.

**Database upgrade in progress** - read only value, used internally by Platform with a cluster environment, when an upgrade is in progress \(when starting up the Platform service\); used to avoid database locked due to multiple nodes started at the same time: only the first setting this flag is granted to continue the upgrade.

**Web Designer activation key path** - optional parameter to use in case no activation key has been uploaded at application level; this is an absolute path in the file system of the Platform server to a folder containing the activation keys.

**Duplicate data per company \(Y/N def. Y\)** - check to use with applications working with multiple tenants: if selected, every time a function is created, it is automatically duplicated for each company id.

**Allow the use of additional filters \(low security\)** - it is strongly recommended NOT to select this checkbox: if you select it, you can pass forward from the UI to the server layer additional SQL conditions which could represent a security leak \(SQL injection\).

**Create EntityManager for additional sources \(list of packages\)** -  ****

**Do not allow to pass a SQL filter on panel loading** - checkbox used to block any additional condition when invoking the standard web service getlist, used to fetch a list of records \(for a grid or a selector\). If not checked, it is allowed to pass a SQL fragment to the base SQL query executed on the server side, which would represent a SQL injection risk.

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

These parameters are also defined at application level.

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

Parameters related to alert messages in case of a cluster based Platform installation \(multiple servers\)

Pre-requisite: the WEB-INF/web.xml file must have been set with "cluster" tag value set to "true"

**Messages messages main node URL** - if set, this public URL will be used to send all notification events; this URL represents the public URL for the main fixed node; use this setting ONLY when you have a cluster where there is a fixed main node; i this parameter is filled, it is 

**Port for the messages main node \(opt.\)** - this parameter must be filled together with the next one: it represents the internal Tomcat port where the main current node is listen for requests

**Protocol for the messages main node \(opt.\)** - this parameter must be filled together with the previous one: it represents the HTTP protocol to use \(http vs https\) to use when communicating with the internal Tomcat where the main current node is listen for requests



### **ALFRESCO** 

parameters related to the ECM module

* Admin Password when connecting to Alfresco Server
* Admin Username when connecting to Alfresco Server
* URL when connecting to Alfresco Server
* sync user in Alfresco
* sync roles in Alfresco
* sync user roles in Alfresco

### \*\*\*\*

### **APP ANALYSIS** 

Parameters related to the tool used to perform an assessment of the app

**Enable application analysis every X hours \(def. disable\)** - in order to start the app analysis, you have to fill in this parameter: this number represents the hours to wait before the next analysis. A good value can be 4 o 8 hours.

**Email used to send notifications after an app analysis** - when the app analysis has started \(through the previous parameter\), Platform can send a notification email with all events analized which overpass the triggers set on the app analysis definition window. This is the email address where the email messages will be sent. Multiple email addresses are supported: use the comma \(,\) symbol to separate each other.

**Destination Phone Nr. when sending SMSs after an app analysis** - when the app analysis has started \(through the first parameter\), Platform can send a notification SMS message with all events analized which overpass the triggers set on the app analysis definition window. You have also to correctly set Twilio parameters for SMS \(see SMS section\). This is the phone number where the SMS messages will be sent.

**Subject to use in SMS/email after an app analysis** - in case of notification by email, this parameter must be filled in as well.

### \*\*\*\*

### **DOCX CONVERSION** 

parameters related to the services which allow to convert documents to the PDF format

### \*\*\*\*

### **EXPORT**

Parameters related to the xls export module

**Export to xlsx using HSSF library \(Y/N def. N\)** - 

**Max number of exportable rows in grid** - 

**Max. nr. of concurrent exports before enqueuing them \(def. 1\)** - 

**Path LibreOffice for export** - 

### \*\*\*\*

### **FILE UPLOAD** 

Parameters used to manage the file upload

**File Storage \(FILE\_SYSTEM or GCS or GDRIVE; def. FILE\_SYSTEM\) File System** - this parameter defines the media to use when uploading files, among the 3 alternative medias: Platform server file system, Google Cloud Storage, Google Drive.

**Default path for directories** - an absolute path to use as base dir for all uploaded files \(for all defined directories\), in case of upload based on file system.

**Google Project Id**  - 

**Create subfolders for company and site \(YN def. Y\)** - 

**Loading directory on startup** - 

**\(opt.\) Autodefine file name for uploaded files** - 

### \*\*\*\*

### **GOOGLE** 

Parameters used to integrate the application with the Google Cloud Platform and the Google Domain \(GSuite\)

**Google Datastore id** **-** in case of app connected to the Google Datastore NoSQL database, this is the Google Cloud Project Id \(mandatory\)

**Namespace list when exporting towards Platform for GA \(, separated\)**  - in case of app connected to the Google Datastore NoSQL database, this is the namespace to use. If not specified, the default namespace will be used.

**Google Service Account Key \(p12 key Base64 encoded\)** - in case of apps connected to any Google Cloud service \(including Google Datastore\), this is the service account key, converted in text \(p12 format, base64\) generated using the Google Cloud Console

**Service Account Email** - in case of apps connected to any Google Cloud service \(including Google Datastore\), this is the service account email generated using the Google Cloud Console; together with the previous parameter, they represent the GCP credentials, essential to access to the GCP services.

**Apps domain admin user for Google Service Account** - in case of apps connected to any Google GSuite service \(now Google Workspace\), this is the service account email generated using the Google GSuite Console

**Google SSO** - **Client id for web application** - 

**Google SSO** - **Client secret for web application** - 

**Google SSO** - **Format to extract username from email** - 

**Google Sync** - **Apps domain to use for synchronization** - the Google Apps domain name \(for example mygoogleappsdomain.com\) from which users and groups must be read. In case of multidomain Google Apps, only the objects of this domain are read. This parameter takes precedence over the next one, customer id.   

**Google Sync** - **Apps customer id used for sync** - in case of multidomain Google Apps, specify the customer id of the Google Apps installation.

**Google Sync** - **User query for synchronization** -  \(opt\) a filter query for users list, as specified in the documentation: [https://developers.google.com/admin-sdk/directory/v1/reference/users/list](https://developers.google.com/admin-sdk/directory/v1/reference/users/list). For example: eMail:a\* to extract only users whose e-mail address starts with “a”.   

**Google Sync** - **Format to extract username from email for sync** - \(opt\) specify this to convert the user email in 4WS.Platform user id. It works like the similar parameter user for SSO. In case of multidomain pay attention that only one parameter can be specified. Default value is {u}. 

**Google Sync** - **Fields extracted from user accounts** - user fields that will be mapped in the destination fields. 

The default value is 

```text
primaryEmail;description;;;
```

The available fields name are specified in Google API documentation \([https://developers.google.com/admin-sdk/directory/v1/reference/users\#resource](https://developers.google.com/admin-sdk/directory/v1/reference/users#resource). 

Use the first level attributes, nested attributes are not supported\) and the following custom values: description, name, surname.  

**Google Sync** -  **Type of fields extracted from user accounts for sync** - user field types used to extract the date. 

The default value is 

```text
UserFormatType;;;;
```

where the first type indicates that the first field is the user name, in string format. The default are string fields. 

**Google Sync** - **Fields extracted from group information for sync** - group fields that will be mapped in the destination fields. 

The default value is 

```text
name;description
```

**Google Sync** - **Type of fields extracted from group information for sync** - user field types used to extract the date. 

The default value is 

```text
;
```

indicating two string fields.

**Google Sync** - **Sync: company, site to use when creating records from Google** - 



\*\*\*\*

### **LDAP** 

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
* \(optional\) Users LDAP filter
* \(optional\) fields to manage in LDAP users
* \(optional\) field types to manage in LDAP users
* \(optional\) LDAP attribute for user id
* Base LDAP path when searching from groups
* \(optional\) Groups LDAP filter
* \(optional\) fields to manage in LDAP groups
* \(optional\) field types to manage in LDAP groups
* \(optional\) LDAP attribute for group id

### \*\*\*\*

### MAIL

The same parameters can also be redefined at application level.

**SMTP host when sending email** - the host name of the SMTP server used to send email messages; this parameter is mandatory; examples: smtp.mandrillapp.com or smtp.gmail.com

**SMTP port when sending email \(opt.\)** - the port used by the SMTP server to accept email messages to send; if not specified, the default port 25 is used; bear in mind that you cannot use the default port 25 if your Platform server has been installed in the Google Cloud Platform, since this port is blocked in the GCP. Moreover, the port also depends on the protocol used: smtp or smtps \(SMTP over SSL\).

**SMTP username when sending email \(opt.\)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**SMTP password when sending email \(opt.\)** - usually an SMTP server requires also credentials in order to accept email messages to send: check it out with the administrator of your SMTP server.

**Use TLS when sending email: E/F \(opt.\)** - allowed values are E or F, i.e. enabled or forced and it depends on the SMTP server settings: check it out with the administrator of your SMTP server.

### \*\*\*\*

### **MOBILE** 

Parameters used to integrate a mobile app with Firebase notification system and other settings.

**Google key for autocomplete place in iOS** - the google key defined through the Google Cloud Console to use the Google autocomplete place API within a mobile app for iOS.

**Google key for autocomplete place in Android** - he google key defined through the Google Cloud Console to use the Google autocomplete place API within a mobile app for Android.



### MONITOR

This section contains settings related to the "monitored services" module of Platform, i.e. the layer intercepting the server-side js action execution, when invoked by the web layer \(web services\), when invoked by the scheduled \(scheduled processes\) or when executed by the queue manager \(enqueued actions\). In all cases, these services are monitored and their execution traced. 

**Email used to send a message, in case of problems on services execution** - this is a mandatory parameter if you have monitored services configured to send notification emails in case of errors during the execution.

**Remote Platform URL n.1...10, used to retrieve log for the monitoring feature** - these 10 parameters can be used to connect the current Platform installation to up to 10 other remote installations, each containing monitored services. Here you have to define the remote URL to Platform installations invoked automatically to retrieve from these remote installations all monitored log and gather it in a unique repository, the current one. 

For more details see:

[https://4wsplatform.gitbook.io/user-guide/modules/ee10-1-log-and-analysis/service-monitoring/remote-platform-servers](https://4wsplatform.gitbook.io/user-guide/modules/ee10-1-log-and-analysis/service-monitoring/remote-platform-servers)

**Wait time before import log \(hrs\)** - a number, expressed in hours, related to the amount of time to wait before automatically retrieve all collected monitored log from the remote Platform installations. This parameter work along with the previous ones.

**Email subject to notify** - the email subject to use when sending notification emails.

### \*\*\*\*

### **PASSWORD** 

Parameters used to define the password policy.

**Password regular expression Password: regular expression explanation** - you can define a regular expression to respect when defining the passwords in the user detail window or when changing password on the login page. 

Example:

```text
^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@$!%*?&])[A-Za-z\\d@$!%*?&]{8,}$
```

**Password: number of days to use for the password expiration** 

**Password: number of erroneous login attempts** - when reached this number for consecutive failed authentications with the same username, the account will be locked. To unlock it, an admin must access the user detail and unlock it.

**Encrypt all passwords \(Y/N\)** - check used to force all passwords defined in PRM01\_USERS to be encrypted. The already existing records with plain passwords will be updated and the PASSWORD field will be a value converted to the encrypted text.

When unselecting this checkbox, all passwords in PRM01\_USERS will be converted to their plain version.

**Number of memorized passwords** - when a password expires, the user if forced to change it and his next access; Platform will not allow the user to type a new password already defined in the past: this parameter defines how many old passwords will be maintained behind the scene and checked to avoid their reuse.

**Send only encrypted passwords to the UI \(def. N\)** - checkbox used to transfer the user list objects and user detail object with the attribute password encrypted, so that it is not possible from the browser inspector to figure out the value of the password by looking at the network layer.

**EMail Template id for resetting password \(example: EN=XXX,IT=XXX or only id for all\)** - a list of template ids, for each language, used when sending an email to the end user who asked for changing password because he forgot his current password.





Application Access

* Enable users
* \(optional\) Access Unavailable message
* Password: number of erroneous login attempts
* Order of Grid Export: ordered list of types export for grids
* Example: XLS\|CSV \(;\)\|CSV \(,\)\|HTML\|PDF\|RTF\|XML \(small format\)\|XML \(large format\)
* Password: number of days to use for the password expiration
* Password regular expression: you can define a regular expression for users password.

  **^\(?=.\*\[a-z\]\)\(?=.\*\[A-Z\]\)\(?=.\*\\d\)\(?=.\*\[@$!%\*?&\]\)\[A-Za-z\\d@$!%\*?&\]{8,}$**

* which means
  * matches a string of 8 or more characters;
  * that contains at least one digit \(d is shorthand for \[0-9\]\);
  * at least one lowercase character and
  * at least one special character and
  * at least one uppercase character.



### **PERMISSIONS** 

Parameters used to define the authentication process

**Show site in users and user roles \(Y/N\)** - checkbox used to define whether the site id column/control must be showed in the users list and in the user detail window. As a default setting, this information is not visible. 

You should check this parameter when you have applications working with multiple site ids.

**Show role id \(Y/N\)** - checkbox used to define whether the role id column/control must be showed int he users list and in the user detail window. As a default setting, this information is not visible and consequently the role id is an auto-generated number reckoned by Platform behind the scenes. 

You should check this parameter only in case you want to be free to define the role id and not let Platform to generate it.

**Show/edit site in user detail \(Y/N\)** - checkbox used to define whether the site id control must be showed and be editable in the user detail window. As a default setting, this information is not visible and consequently the site id to use when inserting records is always the one owned by the current logged user. 

You should check this parameter only in case you want to be free to define the site id and not let Platform to generate it, i.e. when you have applications working with multiple site ids.

**Login controls to hide**  - comma separated list of input fields in the login pane to hide. For example in a Platform installation where there is one only tenant \(one only company id\) or there is only one site id, it is useless to force the end user to specify them each time he logs on and they can be hidden and pre-filled. 

This parameter allows not only to define the list of input fields to hide but also the value to preset for them.

Example:

exit,companyId=00000,siteId=100

The example above would hide the exit button, the company id input field and preset it with a value of 00000, hide the site id input field and preset it with a value of 100.

Allowed input fields that can be hidden:

* companyId
* siteId
* language
* exit

**Check function Ids when reading data \(Y/N def. N\)**

**Automatically create users after successful authentication** - checkbox to select to auto-create a user when logging on \(e.g. when the authentication is managed externally by an LDAP server\).

**Update user from external authentication source \(Y/N\)** - checkbox to select in order to auto-update the user detail starting from data coming from external authentication servers \(e.g. LDAP\); if not selected, users are imported from external system but their data are not updated on time.

**Show only enabled roles** - used in the user detail window: if this checkbox is selected, the list of roles to show is filtered by the roles already owned by the current user; if not selected, all users can see all defined roles at application level, but can only select in the grid \(in edit mode\) the ones owned by the current user.

**Autoassign roles to new user \(';' separated list\)** - in case a user is auto-created when logging on \(e.g. when the authentication is managed externally by an LDAP server\), no roles have been assigned to him yet and consequently, it would not be possible for him to access the application, since two requirements must be fulfilled: a correct authentication + at least one role assigned to the user.

If this checkbox is selected, a user not having roles assigned yet, would inherit automatically the role \(or list of roles separated by a comma\) specified through this parameter and consequently he can access successfully the application.

**Default value for login controls** - ?

### \*\*\*\*

### **REDIS** 

parameters used to manage the integration with a shared cache for user sessions, based on Redis

**Server host name** - required in case of a fixed Redis server

**Server host port** - required in case of a fixed Redis server

**Instance name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the name used to identify the cache name in the Redis server

**Region name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the region name where the Redis instance will be created in the Google Cloud project

**Rest command to create an instance**  - in case of auto creation/destroy of the Google service based on Redis, this is an optional value, expressed in JSON format, related to the BODY content to send to GPC to create the instance

**Interval when Redis is not working** - in case of auto creation/destroy of the Google service based on Redis, this optional value represents the interval \[0-24\] expressed with hours, where the service is not operating

**VPC name** - in case of auto creation/destroy of the Google service based on Redis, this value represents the VPN name used by Redis and by the Compute Engine instances where Platform is running

### \*\*\*\*

### **SCHEDULER** 

Parameters used by the scheduler module

**"From email address" when sending email from Scheduler** - email address used by Platform when sending notification emails for a terminated scheduled process, if the dev has configured a notification at process level. This address will be used as the from address in the email messages.

**Force the main node for scheduled processes to be fixed \(Y or N def. N\)** - in case of a cluster of nodes where one is dedicated to the batch execution \(scheduled processes and enqueued actions\), this checkbox must be selected; moreover, the next parameter must be set as well.

**SCHEDULER\_IP** - the local IP address of the batch node, i.e. the node to use as "main node".



\*\*\*\*

### **UI** 

parameters used by the UI

* Disable GoogleMaps libs loading
* Hide Platform logo
* Max number of exportable row in grid
* Enable users
* Access unavailable message
* Duplicate data per company
* Application activation key path

### \*\*\*\*

###  



