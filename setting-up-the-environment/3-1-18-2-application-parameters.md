# Application parameters

When opening the detail window of a new application, there are two folders available: one contains the settings for the selected application, the other the application parameters, which is an editable grid, where the user can add, change and delete common parameters.  
When saving parameters, these will be accessible from an application when the user will re-logon to the application.  
These parameters are used by specific functionalities of the interpreted application and they are reported in the following list:



#### 4WS.PLATFORM

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



#### ACTIVITI



* Google Maps
  * Start Point Latitude
  * Start Point Longitude
  * Start Point Name
  * Remote Server URL to use in case of 4WS.Platform used on Google App Engine and reports generated remotely in another server
* UI
  * Top menubar
  * First level menu height \(pixel\)
  * Second level menu height \(pixel\)
  * Filter button position \(LEFT/RIGHT\)
* Main UI
  * Number of menu levels
  * Flag to show/hide the menu filter \(true/false\)
  * Status bar height \(pixel\)
  * Top bar height \(pixel\)
  * Menu tree width
  * Show window icon \(Y/N\)
  * Show menu icon \(Y/N\)
  * Buttons menu
  * autosize buttons
  * width/height for buttons
  * width/height for images
  * number of columns to use for buttons layout
  * round border radix for buttons
* Alfresco
  * Alfresco: Admin Password when connecting to Alfresco Server
  * Alfresco: Admin Username when connecting to Alfresco Server
  * Alfresco: URL when connecting to Alfresco Server
  * Alfresco: model file name when connecting to Alfresco Server
* Permissions
  * Login controls to hide
  * Authentication
  * \(optional def. ‘4ws’\) Authentication chain
  * \(optional def. true\) LDAP checking enabled
  * \(optional def. 389\) LDAP port
* LDAP server
  * LDAP account format \(e.g. {u}@domain\)
  * Destinations for the sync process groups/users
  * Sources for the sync process groups/users
  * \(optional def. false\) Logical delete of users before sync
  * \(optional def. tutte\) company/site couples to use when creating records
  * \(optional\) fields to manage in 4WS users table
  * \(optional\) fields to manage in 4WS groups table
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
* Scheduler
  * "From email address" when sending email from Scheduler
* Email notification system
  * SMTP host when sending email
  * \(optional\) SMTP port when sending email
  * \(optional\) SMTP protocol when sending email
  * \(optional\) SMTP username when sending email
  * \(optional\) SMTP password when sending email
  * \(optional\) Use TLS when sending email: E/F
* Application Access
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
* Customize Datastore

First, create a server side javascript action when defining the custom logic; this action receives in input the **dataStoreId** value \(in the **reqParams** input object\) and the current user and other user information \(contained in the userInfo input object\). 

You can use this information to decide which datasource to return back, through the **setReturnValue**\(\);

Finally, it is possible to define a custom logic to figure out which additional datasource to use, according to the user. For instance, if you have a table reporting which datasource to use for each user, you can define a server-side javascript action and use it to dynamically decide the additional datasource to use.

Second, fill in the action id just defined as the “Customize Datastore” application parameter.

## Example

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

