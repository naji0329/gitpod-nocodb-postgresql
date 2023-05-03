# nocodb-postgresql-gitpod
Gitpod workspace definition with NocoDB and PostgreSQL

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/lucasjellema/nocodb-postgresql-gitpodnocodb-postgresql-gitpod)
nocodb-postgresql-gitpod

The workspace includes services PostgreSQL (open source database) and nocodb ( a no-code database platform that allows teams to collaborate and build applications with ease of a familiar and intuitive spreadsheet interface) . These are started when the docker-compose.yml file is started - which happens when the workspace is launched.

When the containers are all running, on port 28276 we can open the `nocodb` web ui. After creating an account, you can enter the tool. Under `Team & Settings` create a new data source that connects to the demo user and the demodb database and the demo schema. Subsequently I can add tables in the project under this data source - and "pick up" tables that already exist in the database.

![](images/data-source-postgresql.png)


I can define new tables, enter data and create a view on that data. I can even share that view (a web page) with anyone on the public internet.

One way to look inside the PostgreSQL database is with the CLI *pgcli*. It is opened in a second terminal, using
```
pgcli 'postgres://demo:abc123!@localhost:5432/demodb'
```

List tables:

```
\dt
```

Create a table through DDL in this CLI and the table becomes available for NocoDB to use in the application. Tables can be created from either end (NocoDB UI and directly in the database) and the same applies to data.
