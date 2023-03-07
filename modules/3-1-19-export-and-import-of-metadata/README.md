# Export and Import of Metadata

Metadata defines the application, in terms of UI, server-side components, events, application behavior.

A common approach when using Platform is to configure the application in a development environment and then publish the application in a production environment.

Platform provides a feature to publish metadata from an environment to any other.

There is a requirement which must be respected: metadata can be exported from an environment to another **only for environments having the same Platform version**. That means both dev and prod environments must share the same version of Platform.

The publication process consists of **exporting metadata** from the starting env and **importing** it on the target environment.

In order to export metadata, you have to work on the starting environment where you can use “Import/Export Application” functionality, available in the **Application** menu.



## Exporting all metadata

Through the “Metadata application management” folder, you can export metadata: you have just to press on the “**Export Application**” button and wait for the .zip file produced by Platform. This .zip file can be downloaded and saved on your local file system.

Moreover, it is strongly recommended to pay attention to the **languages to export**: **** it can happen that you are developing a multi language product and you have define many languages, but only a few of them are actually used in the target env where you wanna import metadata; in such a case, you'd better not to export all languages, but only the ones actually used. This approach can **significantly reduce the amount of time required to import metadata in the target environment**.

Once done that, you are ready to import metadata by working on the target environment: open the same functionality and, this time, upload file .zip file previously exported in the “Application to upload” input field and press “Import Application” button.

<figure><img src="../../.gitbook/assets/image (9) (2).png" alt=""><figcaption></figcaption></figure>

Before doing it, you can optionally set a few settings just below the input field:

* **Delete old data** - check box used to replace all previously metadata from the target environment and to the new ones; this is the predefined choice and it should NOT be unchecked.
* **Company id to use in import** - combo box used to select the company id (tenant) to use when importing metadata. Note that metadata is related to (i) the application which is independent of the company id and (ii) users/roles and other data depending on the specific company id. Consequently, when importing metadata, you are replacing the application for all company ids, since it is common to all company ids and, you are importing specific metadata for a single company id, the one selected.
* **Copy for all companies** - check box used to for the metadata import for all company ids: in such a case, this setting will override the combo box described above.&#x20;
* **Progressives** - check box used to define whether the metadata import includes also all internal progressives coming from the source environment. Note that it is not a good idea to import them, since they should be different for each environment.
* **Roles** - check box used to define that metadata import is also about roles coming from the source environment.

Note that it is not a good idea to import them, since they should be different for each environment.

* **Users** - check box used to define that metadata import is also about users coming from the source environment. If “Roles” check box has been selected too, the association between users and roles are imported as well.

Note that it is not a good idea to import them, since they should be different for each environment.

* **Custom translation** - check box used to define that also custom translations must be imported. Usually this is not required, since custom translations should be specific for each environment.
* **Mobile theme** - check box used to define whether the mobile theme should be imported as well, in case of a mobile app.

This window is shown by pre-setting the most common import configuration, so that you should not need to change any setting and just upload the file and press “Import application”.

Actually, this button will not directly start the import process, but only start a checking over the content of the .zip file: the purpose of this checking is described below.



When the import process has been started through the “Import application” button, Platform will analyze the .zip content, searching for metadata which can have differences according to the environment. It is possible that you don’t want to import all of them and Platform will show you all these differences, organized per topic.

![](https://lh6.googleusercontent.com/mCI-1W4Q4Vmv2jH134eDs4ogiFTyV41DAr4oGkF10xm9spRKCX-ZfhHWZ7aypnKNRvdbzMkTasrNJoSAjAxWcOm9RTvFMKcCEwxvYba7U1CpHZ0zF9-86rdc\_p9UpLx0aZ3YiVB9)

Platform analyze these topics:

* additional data sources
* application parameters
* global parameters
* directories
* permissions, in terms of users and roles
* custom translations
* templates
* off-line parameters used by the off-line component
* mobile themes

For each of them, all related records are reported with the previous value (when available) and the value to set on the import process.

You can uncheck any of these records, if you want to by-pass their import.

In this way, you have a full control over the env-dependent-settings to include/exclude.

Please note that all new parameters should be imported and you should fill in them or replace the previous value, to set a valid value according to the target environment.

At this point, you can press the “**Import application**” button to the bottom of the window to start the real import process.

At the end of the import process, Platform prompts the user about two optional tasks:

* **re-activate datasources** - in case new data sources have been imported, you have to confirm this activity, so that these data sources will be enabled and be ready to use.
* **objects checking** - this is the same operation described before when talking about the button named “Verify objects” .



## **Additional buttons**

A few additional operations are available, apart form the metadata export:

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

* **Verify objects** - button used to compare the tables descriptions coming from the metadata and the real definition of tables: this feature can be helpful in case of an erroneous disalignment between two environments, to find out the inconsistencies.
* **Create/Align tables in BigQuery** - button used to optionally check out the tables that must be defined in BigQuery, compared with the metadata: if there are BigQuery type objects included in the metadata and not yet created as tables in BigQuery, there are automatically created. Same for fields disalignments.
* **Create tables after importing data** - button used to optionally create missing tables starting from the metadata definition; pay attention to this operation: it could not be a good idea to depend on this feature to align two distinct databases, but it can come in handy to quickly and temporarelly fix a disalignment in a production environment.
* **Export metadata to Platform for GAE** -  this button is visibile only for app configured to be executed within the Google App Engine Container; in such a scenario, you configure the app using the App Designer running on Platform Standard and then export it inside GAE, in order to run the application in this container.
* **Compare metadata with a remote environment** - this feature can be used as an alternative to export all metadata (described in the previous section). Through this feature, it is possible to select single parts of metadata and publish them in another environment. It can be helpful to publish for example fixes or specific new parts. Additional information about this feature is reported in the next section.



## **Compare metadata with a remote environment**

&#x20;This feature allows to compare local metadata (e.g. coming from the development environment) with metadata coming from a remote installation (e.g. production environment).

<figure><img src="../../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

When opening the window, local metadata is automatically loaded. In case there are changed in metadata performed in the last few minutes, it is possibile to press again the "**Local metadata reload**" button to refresh local metadata.

When pressing the "**Fetch remote metadata**" button, a dialog is prompted to the user, in order to connect to the remote installation:

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

The base URL to the Platform installation must be specified, along with the credentials to access to the App Designer, using a remote user enabled to access to the App Designer to publish metadata.

Once pressed the "Metadata remote import" button, metadata is retrieved from the remote server. After that, the comparison between local and remote metadata is automatically started. The time required to do it can changes according to the dimension of the app, from a few seconds up to a minute.

Once completed the comparison, a tree is rendered, showing only new/changed metadata, available in the local env but not in the remote env:

<figure><img src="../../.gitbook/assets/image (12) (2).png" alt=""><figcaption></figcaption></figure>

Instead of showing new/changed metadata in a plain list, it is grouped hiearchically, in order to make it easier for the dev to figure out all metadata to send, related to a specific functionality.

For example, in case of a new menu item opening a new window composed of panels, events, actions, linked to a business component and object, the root node is a PRM04\_FUNCTIONS (menu item), whose child is a window, containing sub-nodes which are panels, columns, controls, events, actions, etc.

It is up to the dev to figure out exactly what to export.

To facilitate such task, there is a filter panel where filtering content by:

* date interval
* user
* metadata type (new, changes)
* component type (panel, actions, etc.)

The tree-grid provides the following information:

* id - the unique identifier of the metadata (e.g. panel id for a panel, etc.)
* sel - checkbox used to select which metadata to export
* type - metadata type (e.g. panel, column, etc.)
* title - metadata title, when available (e.g. window title, panel title, b.c. title, action title, etc.)
* operation - new or changed metadata&#x20;
* create user/datetime - the user/date creating the metadata in the local env
* last update user/datetime - the user/date updating for the last time the metadata in the local env

Moreover, when the dev clicks on a check node to select what to export, all subnodes are automatically checked too, in order to reduce the chance to have inconsistencies when exporting data.

**Important note**: pay attention to ehat you are exporting: it is possible that the export ends with an error due to foreign keys violated, because the metadata selected is not all needed: for that reason there is the automatism  to auto-select checkboxes to subnodes.

Anyway, there are more subdle cases where there are dependecies not depending on the FK, as for a client side action invoking a server-side action: it is up to the dev to know that and take it into account, during the selection process.



Finally, when pressing the **Metadata** **Export** button, the remote export is started.

The **History** button shows all previous exports correctly finished, in order to figure out what was exported in the past and by whom:

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

When double clicking on a row, a detail window is shown, where the report of all metadata exported is prompted:

<figure><img src="../../.gitbook/assets/image (4) (4).png" alt=""><figcaption></figcaption></figure>

