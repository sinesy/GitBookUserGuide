# Access Log



This feature automatically collects every login attempt to a web application, both successfull and failed logons. More precisely, only failed logons due to matching with the black list feature are logged.

In the **Access Log** tab, a few information are reported:

* Application id
* User id: company id + site id + username
* Access log date and time
* Event type: LOGIN
* browser IP
* Checkbox - selected when the login failed due to back list policy matching

![](<../../.gitbook/assets/image (21).png>)

Moreover, the client time zone is also saved, along with the other data reported above, in the CON60\_LOGS table.



Additionally, it is possible to get additional information about a specific user, through the Log **Access Duration tab**:

![](<../../.gitbook/assets/image (19).png>)

In this window, you have first to fill in the username input field and press Search.

The grid would show the list of all access attempts for that user and its duration (login and logout date+time).



### Black list policy

Optionally, it is possible to fine tune the login access policy, by specifying a server-side javascript action, defined per application, invoked just after a valid login and use it to cancel the login attempt.

In this action, you have a few data in input, available through the **reqParams** and **reqHeaders**: they are inherited .by the HTTP request coming from the web login page. As a consequence, you have access for example to:

* reqParams: companyId, siteId, username, clientTimeZone
* reqHeaders: X-Forwarded-For, User-Agent&#x20;

The action response allows to interrupt the login process and provide an error message.

Such an error is automatically logged in the Access Log feature.

In order to activate such a policy, you have to define the Application Parameter named "**Server-side action before login**" available in the group LOGIN, filled with the action id.

Example of server-side javascript action:

```
if (reqParams.username=="ADMIN") {
    utils.setReturnValue(JSON.stringify({ 
      success: false, 
      message:"You are not allowed to access" 
    }));
 }
```

Thanks to the data provided in input, it is possible for example to create a black list based on:

* specific IP addresses (using reqHeaders\["X-Forwarded-For"] IP address)
* specific browsers (using reqHeaders\["User-Agent"] browser description)
* access time (testing current time)
* specific users (testing reqParams.username)

and much more.







