# Create an Amber Application

- [Create an Amber Application](#create-an-amber-application)
    + [Bootstrap an Application](#bootstrap-an-application)
    + [Installing Dependencies](#installing-dependencies)
    + [Creating the database](#creating-the-database)

Before we begin, please take a minute to read the [Installation Guide](getting-started/Installation/README.md). By installing any necessary dependencies beforehand, we’ll be able to get our application up and running smoothly.

At this point, we should have Crystal and Amber installed. We should also have PostgreSQL and NodeJS installed to build a default application.

To verify you have Amber installed, run the command `amber -v` in your terminal window:

```bash
$ amber -v
Amber CMD (amberframework.org) - v0.2.6
```

### Bootstrap an Application

To bootstrap your Amber application, run `amber new` with an absolute or relative directory path to the application directory it should create. Assuming that the name of your application is "weblog", let's run:

```bash
$ amber new weblog
```

Additionally, the following options may be passed to the above command:

* `-d` This specifies the database driver to use. It defaults to pg, for PostgreSQL.
* `-t` This specifies the template rendering engine. It defaults to slang, the Slim-inspired templating language.
* `--deps` This will download and install project dependencies for you, to save the additional step of having to type `shards install`.


Amber generates the [directory structure](/guides/getting-started/Installation/directory-structure.md#directory-structure) along with files necessary for the application.


Change your current directory to `weblog`, if that was the path you chose:

```bash
cd weblog
```

### Installing Dependencies

Now install project dependencies with `shards install`:

```bash
$ shards install
Installing amber (0.2.6)
Installing radix (master)
Installing kilt (0.3.3)
Installing slang (master)
...
Installing sqlite3 (0.8.2)
Installing granite_orm (0.7.3)
Installing quartz-mailer (0.1.0)
Installing smtp (master)
Installing jasper_helpers (0.1.5)
Installing amber_spec (0.1.1)
```

### Creating the database

Amber makes it easy to interact with your database. Amber supports Postgres, MySql, and Sqlite.

Edit the database setting for your current environment by editing {project_name}/config/environments/{current_environment}.yml file. Amber looks at the database_url key for the default database connection string.

> Amber assumes that your PostgreSQL database will have a `postgres` user account with the correct permissions and no password set for this user. If that isn’t the case, update the `database_url` key `config/environment/{current_environment}.yml` with the correct database credentials for your environment.

With your database credentials ready, run the following command in your terminal window:

```bash
amber db create
```

This creates your application's Postgres database. It should output:

```bash
Created database weblog_development
```

And finally, we’ll start the Amber server:

```bash
amber watch
```

By default Amber accepts requests on port 3000. If we point our favorite web browser at [http://localhost:3000](http://localhost:3000), we should see the Amber Framework welcome page.

![amber-welcome](https://raw.githubusercontent.com/amberframework/site-assets/master/images/amber-framework-welcome.png)

If your screen looks like the image above, congratulations! 

You now have a working Amber application. If you don’t see the page above, try accessing it via [http://127.0.0.1:3000](http://127.0.0.1:3000).

Locally, the application is running in a Crystal process. To stop it, we hit ctrl-c once, just as we would terminate the program normally.

> **Note:** The **amber watch** command uses [Sentry](https://github.com/samueleaton/sentry) to watch for any changes in your source files, recompiling automatically. If you don't want to use Sentry, you can compile and run manually:  
> 1. Build the app `crystal build --release src/[your_app].cr`  
> 2. Run with `./[your_app]`  
> 3. Visit `http://0.0.0.0:3000/`



