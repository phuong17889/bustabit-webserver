INSTALLATION
============

Debian/Ubuntu 16
-------------

These are instructions for running bustabit locally on a Debian / Ubuntu machine.

### Distribution packages

You will need to install the Postgres DBMS and node.js. The `nodejs`
package installs `nodejs` but will additionally create a symlink from
`/usr/bin/node` to `/usr/bin/nodejs`.

    curl -fsSL https://deb.nodesource.com/setup_0.12 | sudo -E bash -
    sudo apt install git npm postgresql nodejs libpq-dev python-psycopg2 postgresql-server-dev-all

### Install plv8
```
cd /tmp
wget https://github.com/plv8/plv8/archive/v2.0.0.tar.gz
tar -xvzf v2.0.0.tar.gz
cd plv8-2.0.0
make static
make install
```

### Getting the sources

    git clone https://github.com/phuong17889/bustabit-webserver.git
    cd bustabit-webserver

### Create a database user and setup the tables

Create a user. It will prompt you for a password.

    sudo -u postgres createuser -P bustabit

Create the database and setup the tables. The second command will prompt you
for the password again.

    sudo -u postgres createdb -O bustabit bustabitdb
    sudo -u postgres psql -W -U bustabit -d bustabitdb -h localhost -f server/sql/schema.sql


Configuration
=============

### Installing node.js dependencies locally.

This will download and install all dependencies in the `node_modules` subdirectory.

    npm install

### Database

Export the database link as an environment variable

    export DATABASE_URL=postgres://bustabit:<YOURPASSWORD>@localhost/bustabitdb

### BIP32 Key

You will need to create a BIP32 key pair. You can do at your own risk online at [bip32.org](http://bip32.org/). Export the public key as an environment variable

    export BIP32_DERIVED_KEY=xpub6AH.....


Running
=======

You can run the server by using `npm start`. By default, it will listen on port `3842`.
