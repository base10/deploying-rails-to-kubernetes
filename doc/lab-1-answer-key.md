# Lab 1 - Prepare for ephemeral infrastructure

## Overview

In this lab we will configure our small Rails app to connect to a database and
Redis server running in the VM.

## Procedure

### Step 1 - Change DB config

In the Rails app, modify `config.database.yml` as follows:
1. Comment out the line

`database: link_development`

2. Add this new line instead

`url: <%= ENV.fetch("DATABASE_URL", "") %>`

### Step 2 - Transfer data to VM database

1. Export a database dump from your local environment and save it to a file in
the `vagrant\data` folder. For example, you might use this command if you are
currently outside the `deploying` repo folder:

`pg_dump link_development > deploying-rails-to-kubernetes/vagrant/data/link_development.sql`

2. Log into the datastores VM:

`vagrant ssh workshop_datastores`.

3. Switch to the postgres user:

`sudo su - postgres`

4. Connect to the postgres database and create the `link` database with:

```
psql
create database link;
\c link
exit
```
5. Import the data:

`psql link < link_development.sql`

6. Confirm that the data is present:
```
psql
\c link
select * from users;
select * from entries;
```
### Step 3 - Configure DB to accept connections from outside the VM

Note that this step is insecure and should be used only in a limited test env.

1. Edit `postgresql.conf`:

`sudo vim /etc/postgresql/12/main/postgresql.conf`

2. Find the property labeled `listen_addresses` and change the value from
`localhost` to `*`:

`listen_addresses: '*'`

3. Edit `pg_hba.conf`:

`sudo vim /etc/postgresql/12/main/pg_hba.conf`

4. At the end of the file, add these two lines:

```
host    all             all             172.16.100.1/32         trust
host    all             all             172.16.100.10/32        trust
```

5. Restart the Postgres service:

`sudo service postgresql restart`

### Step 4 - Configure Redis to accept connecvtions from outside the VM

Note that this step is insecure and should be used only in a limited test env.

1. Edit `redis.conf`

`sudo vim /etc/redis/redis.conf`

2. Find the `bind` directives and add a new line:

`bind 172.16.100.20`

3. Find the `protected-mode` property and change it from `yes` to `no`:

`protected-mode no`

4. Restart the Redis service:

`sudo service redis restart`

### Step 5  - Add environment variables

Add these two lines to the `.env` file in your application:
```
DATABASE_URL=postgresql://postgres@172.16.100.20:5432/link
REDIS_URL=redis://172.16.100.20:6379/15
```

### Step 6 - Test

Start the application and visit it in a browser to confirm things are running as
expected. Visit the `/sidekiq` route and confirm that the Redis URL at bottom of
the page is the one from the environment variable.
