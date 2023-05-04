# nocodb-postgresql-gitpod
Gitpod workspace definition with NocoDB and PostgreSQL

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/lucasjellema/nocodb-postgresql-gitpod)

The workspace includes services PostgreSQL (open source database) and nocodb ( a no-code database platform that allows teams to collaborate and build applications with ease of a familiar and intuitive spreadsheet interface) . These are started when the docker-compose.yml file is started - which happens when the workspace is launched.

![](images/workspace-overview.png)

NocoDB is a no-code database platform that allows teams to collaborate and build applications with ease of a familiar and intuitive spreadsheet interface. This allows even non-developers or business users to become software creators.

NocoDB works by connecting to any relational database and transforming them into a smart spreadsheet interface! This allows you to build no-code applications collaboratively with teams. NocoDB currently works with MySQL, PostgreSQL, Microsoft SQL Server, SQLite, Amazon Aurora & MariaDB databases. This workspace uses PostgreSQL.

Also NocoDB's app store allows you to build business workflows on views with combination of Slack, Microsoft Teams, Discord, Twilio, Whatsapp, Email & any 3rd party APIs too. Plus NocoDB provides programmatic access to APIs so that you can build integrations with Zapier / Integromat and custom applications too.

The workspace will appear in the browser like this:
![](images/running-workspace.png)

When the containers are all running, on port 8080 we can open the `nocodb` web ui. 

Create a new (admin) account: enter a valid email address as user account, a password and click on *Sign Up*.
![](images/create-account.png)

After creating an account, you get to the welcome page where a list (zero) projects is shown. Click on *New Project* to create a new project.
![](images/new-project.png)

Enter the name for the project and click on *Create*.
![](images/create-project.png)

We now want to create a connection with the *demodb* database and *demo* user in the PostgreSQL database. The two databases (postgres and demodb) are used for the nocodb metadata and the application tables respectively.

In the overview page, click on Team & Settings
![](images/click-teams.png)
Click on *Data Sources* and on *New* to create a new data source that connects to the demo user and the demodb database and the demo schema. 
![](images/new-datasource.png)

Enter the details for this data source:
* Base Name - anything you like
* Database Type - PostgreSQL
* Host Address - postgresql
* Port number - 5432
* Username - demo
* Password - abc123! 
* Database - demodb
* Schema name - public 

![](images/new-datasource-details.png)

Press *Test Database Connection*. When successful - no typos etc - click *OK & Add Base*.

Subsequently I can add tables in the project under this data source - and "pick up" tables that already exist in the database.

Click on the button *ERD* for the new database connection - to list all current tables in the database (of which there are none):
![](images/open-erd.png)

The ERD is presented - empty for now.
![](images/show-erd.png)

I can define new tables, enter data and create a view on that data. I can even share that view (a web page) with anyone on the public internet.

Let's create a table in the database - to find out how nocodb can leverage an existing database with tables and data.

We will now look directly inside the PostgreSQL database using the CLI *pgcli*. It is opened in a second terminal, using
```
pgcli 'postgres://demo:abc123!@localhost:5432/demodb'
```
List tables:

```
\dt
```

Create a table through DDL in this CLI and the table becomes available for NocoDB to use in the application. Tables can be created from either end (NocoDB UI and directly in the database) and the same applies to data.

In *pgcli* enter this SQL statement:
```
create table countries (name VARCHAR(100), code VARCHAR(3), population INTEGER);
insert into countries (name, code, population) values ('The Netherlands', 'nl', 18456789);
```
![](images/create-table.png)

The table exists, has one record of meaningful data in it. Let's see how to use it in nocodb.

Back to the browser and the nocodb application.

Click on *Sync Metadata* for the data source.
![](images/sync-metadata.png) 

The Metadata tab will indicate that a new table was found in the data source:
![](images/meta-sync-result.png)

Click on *Sync Now* to import the new table's definition into nocodb and make it available for use in the application. Note: this is where your complete preexisting datamodel with dozens or hundreds of tables and views can be identified, scanned and added to the nocodb repository.

The result of this sync is presented:
![](images/after-sync.png)

Return to the Data Sources Tab and click on *ERD* for the connection to user *demo* in *demodb*.
![](images/new-erd.png)

The table is now included in the ERD.

Close the popup. In the left hand pane, open the node for the data source (*electronic-tiger* in the example). The table *Countries* should be listed. Click on it to see its definition. 
![](images/table-countries-in-nocodb.png) 

At this point, I will let your imagination, the documentation for Nocodb, [live demos](https://docs-prev.nocodb.com/getting-started/demos/) and other tutorials take over. Creating a view on top of this table is trivial. Creating additional tables - that may link to COUNTRIES - is also straightforward. 

# Resources

[NocoDB documentation](https://docs.nocodb.com/)
[NocoDB GitHub](https://github.com/nocodb/nocodb)
[NocoDB Live Demo](https://docs-prev.nocodb.com/getting-started/demos/)