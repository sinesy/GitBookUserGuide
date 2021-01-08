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

parameters related to the tool used to perform an assessment of the app

### \*\*\*\*

### **DOCX CONVERSION** 

parameters related to the services which allow to convert documents to the PDF format

### \*\*\*\*

### **EXPORT**

parameters related to the xls export module

### \*\*\*\*

### **FILE UPLOAD** 

parameters used to manage the file upload

### \*\*\*\*

### **GOOGLE** 

parameters used to integrate the application with the Google Cloud Platform and the Google Domain \(GSuite\)

* Apps domain admin user for Google Service Account
* Service Account Email
* Service Account Key
* Google SSO
* Client id for web application
* Client secret for web application
* Format to extract username from email
* Apps domain to use for synchronization
* Apps customer id used for sync
* Google Sync
* User query for synchronization
* Format to extract username from email for sync
* Fields extracted from user accounts
* Type of fields extracted from user accounts for sync
* Fields extracted from group information for sync
* Type of fields extracted from group information for sync
* Sync: company, site to use when creating records from Google

### \*\*\*\*

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

### **Email notification system**

* SMTP host when sending email
* \(optional\) SMTP port when sending email
* \(optional\) SMTP protocol when sending email
* \(optional\) SMTP username when sending email
* \(optional\) SMTP password when sending email
* \(optional\) Use TLS when sending email: E/F

### \*\*\*\*

### **MOBILE** 

parameters used to integrate a mobile app with Firebase notification system

### \*\*\*\*

### **PASSWORD** 

parameters used to define the password policy

* Password regular expression: you can define a regular expression for users password
* Password: number of days to use for the password expiration
* Password: number of erroneous login attempts



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

* Login controls to hide
* Encript all passwords
* Authentication chain
* Authentication types in login dialog
* Destination for the sync process groups/users
* LDAP sync also groups
* Synchronization
* Logical delete of users before sync
* Company, site couples to use when creating records
* Fields to manage in 4WS users table
* Fields to manage in 4WS groups table
* LDAP user name/surname for email format
* SSO
* URL server
* Manager class name
* Parameter name id user SSO
* Parameter name token SSO

### \*\*\*\*

### **REDIS** 

parameters used to manage the integration with a shared cache for user sessions, based on Redis

* Server host name - required in case of a fixed Redis server
* Server host port - required in case of a fixed Redis server
* Instance name - in case of auto creation/destroy of the Google service based on Redis, this value represents the name used to identify the cache name in the Redis server
* Region name - in case of auto creation/destroy of the Google service based on Redis, this value represents the region name where the Redis instance will be created in the Google Cloud project
* Rest comand to create an instance  - in case of auto creation/destroy of the Google service based on Redis, this is an optional value, espressed in JSON format, related to the BODY content to send to GPC to create the instance
* Interval when Redis is not working - in case of auto creation/destroy of the Google service based on Redis, this optional value represents the interval \[0-24\] expressed with hours, where the service is not operating
* VPC name - in case of auto creation/destroy of the Google service based on Redis, this value represents the VPN name used by Redis and by the Compute Engine instances where Platform is running

### \*\*\*\*

### **SCHEDULER** 

parameters used by the scheduler module

* "From email address" when sending email from Scheduler
* * Collaboration
* URL 4WSMonitor
* Show role id
* Show site id in users/user roles
* show/edit site id in user detail
* day number of log

### \*\*\*\*

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



