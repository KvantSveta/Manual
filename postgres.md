# Postgres


**install postgres and first settings**
```bash
sudo apt-get update
sudo apt-get install postgresql-9.4

sudo -u postgres psql
\password postgres
Enter new password:
Enter it again:
```

**connect to postgresql via postgres**
```bash
psql -h localhost -U postgres
Password for user postgres:
```

**create user, database and grant privileges**
```bash
sudo -u postgres psql
create user sakura with password 'password';
create database sakura_db;
grant all privileges on database sakura_db to sakura;
\q
```

**connect to postgresql via sakura**
```bash
psql -h localhost -d sakura_db -U sakura
Password for user sakura:
```

**reinstall postgres**
```bash
sudo apt-get remove --purge postgresql-9.4
sudo apt-get install postgresql-9.4
```

**install postgres from source files**
```bash
./configure
make
sudo make install
sudo adduser postgres
sudo mkdir /usr/local/pgsql/data
sudo chown postgres /usr/local/pgsql/data
sudo -u postgres /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
sudo -u postgres /usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data>logfile 2>&1 &
/usr/local/pgsql/bin/createdb test
/usr/local/pgsql/bin/psql test
```
