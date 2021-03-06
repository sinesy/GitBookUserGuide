# Datastore statistics

This form allows to see all operations applied on the Google Datastore, in terms of reading entities, writing entities \(inserts/updates\), deleting entities.

Data is gathered for each:

* company id
* application id
* day+month+year
* entity

It is possible to search for a specific company/app id or day.

Month and years are mandatory.

![](../../.gitbook/assets/schermata-2020-10-12-alle-15.53.07.png)

Data is automatically collected when using panels connected to Datastore, export SQL tables to datastore, when using any of the utils.xxx methods working on Google Datastore.

Data is retrieved in near real time and saved every 5 minutes.

