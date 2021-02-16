# File Management

There is always the chance to add additional files to the application configured using the App Designer. In that case, a series of custom files can be created and should be stored inside the application subfolder. The file system has this organization:  
**tomcat -&gt; webapps -&gt; platform -&gt;applicationsubfolder**  
When creating a new application through the App Designer, the user specifies an "applicationsubfolder" for that application; when saving these settings, such a folder will be created by the App Designer within the "platform" web context of the Application Server \(i.e. Tomcat\).  
The subfolder should respect this structure:  
/ **script** – custom javascript files  
/ **css** – custom CSS files  
/ **xyz** – any other static or dynamic content accessible through the web

When starting the web application, the Web interpreter will automatically scan this subfolder searching for .js/.css files and it will include all of them along with the rest of the application; in this way you can attach any custom GUI content.  
When starting the mobile app, the Mobile Interpreter will automatically receive the content of this subfolder , which should contain static content like images or documents which should be downloaded and used locally by the mobile app; in this way you can attach any custom GUI content.  
Java source classes created by the programmer need to be included with respect to the Eclipse IDE source folders structure. Consequently, you can create an additional source folder, such as "srcCustomizations", and add to it any source file you want, related to Resource classes, ending with Resource or business components ending with Bean and respecting the correct syntax of EJB 3 Stateless Beans.  
Also you can manage translated messages on server side with invocation of class WAGInternalState, recovering file ".properties" loaded into the subfolder of application.  
These classes will be automatically recognized by the web container \(Tomcat\) when starting it. That means that you need to restart the A.S. any time you change these classes \(unless you’re starting Tomcat from within the IDE, using the debugger feature that allows a live updated of java classes\).  
When you are ready to publish these custom files to another environment, you have to copy the classes and reports within the /WEB-IN/classes subfolder.  
For instance, you could create an Ant task \(a build.xmlfile\) to do that.  
After doing that, you can publish them into the applicationsubfolder in two alternative ways:

* using the  **Administration -&gt; File Manager**  – here you can select the root node of theapplicationsubfolder and upload a single file in that folder \(or in any subfolder by selecting it\) by choosing it in the “File to upload” input field and pressing the corresponding “Save” button. If you have multiple files to publish, you can first create .zip file on your local file system, including all the files to publish and then choose “. zip file to upload” andpress the corresponding “Save” button

![](http://4wsplatform.org/wp-content/uploads/2018/01/filemanager.png)

* Using the  **Application -&gt; Import/Export Application**  – in the first folder, named “File Management”, you can upload a .zip file including all the content you need to publish and then press the “Import files” button. 
* According to the application type \(web vs mobile\), there can be additional settings available: "**Save context on DB**" checkbox allows to save the zip file also into the database; in this way, in case of a cluster environment, files are replaced on the file system with the ones saved in the database, each time a new instance node is created, without having to regenerate the instance template only because some files have changed. DO NOT check it if you do not run your application in a cluster. DO NOT check it in your dev environment.

![](../.gitbook/assets/schermata-2021-02-16-alle-16.55.02.png)

* In case of a mobile app, it is also possible to select **which context to work with**: a mobile app has two contexts
  * a web context, used when accessing the web front-end executed in the Platform server; this is rarely used, typically when roles and users must be defined
  * a mobile context \(images, etc.\) sent to a mobile app, each time a synchronization process is executed  and such a context has changed in some way.

![](../.gitbook/assets/schermata-2021-02-16-alle-16.54.31.png)



**Note** : That .zip file can then be used to import .class or report files. Once launched the import process, the App Designer will recreate the original structure of the custom files, by moving any .classes and .report file it finds to the correct classpath. Remember to restart the web container in order to make Tomcat able to find and load these classes.

