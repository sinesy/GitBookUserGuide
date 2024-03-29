# Server-side Javascript

You can find the complete reference about server-side Javascript in the API Documentation, through this [link](https://4wsplatform.gitbooks.io/api/content/Email.html)

By and large, a server-side javascript action (or GAE action) allows to access to all resources provided by the server, including:

* database
* NoSQL database
* web services
* local or on the cloud file system

The editor is the same for all javascript actions and it provides:

* syntax checker
* line number
* syntax highlithers
* **auto completion function**, accessible by typing a few character and then pressing CTRL+space (or COMMAND+space); this feature shows all compatible predefined functions provided by Platform
* **code generator which provides javascript code for an object** (data model) definition, in terms of attributes, accessible by pressing CTRL+I (or COMMAND+I); this command prompts the user with a dialog reporting all defined data models: once selected one the corresponding attribute definition is pasted within the js editor.

**Important note:** the source code written within a server-side action should be **organized in many functions and a little amount of executable commands**, which should be focused on function calls. In this way, the total source code would not create memory problems due to "source code exceeded 64k" and the code is also more compatible with the unit test.



