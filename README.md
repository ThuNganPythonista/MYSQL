# MYSQL

**MySQL is open source database management software, helping to store, organize, and retrieve data. In the process of using MySQL, users need to master a few common and important commands. For each command, before executing, the user needs to log in to MySQL with the root account (MySQL root, not the VPS management root account) or an account with full rights.**


**All commands below are operated by the instructor on a CentOS VPS.**

**1, Directory containing Database**

- Log in to MySQL: mysql -u root -p
- All raw database files on CentOS, stored in directory: /var/lib/mysql

**2, Account management and authorization**

Show all users:

`mysql> SELECT * FROM mysql.user;`

Delete null users:

`mysql> DELETE FROM mysql.user WHERE user = ' ';`

Delete all users that are not root:

`mysql> DELETE FROM mysql.user WHERE NOT (host="localhost" AND user="root");`

Rename the root account (helps with security):

`mysql> UPDATE mysql.user SET user="mydbadmin" WHERE user="root";`

Assign full rights to a new user:

`mysql> GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' IDENTIFIED BY 'mypass' WITH GRANT OPTION;`

Detailed permissions for a new user:

`mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES ON mydatabase.* TO 'username'@'localhost' IDENTIFIED BY 'mypass';`

Assign full rights to a new user on a certain database:

`mysql> GRANT ALL PRIVILEGES ON mydatabase.* TO 'username'@'localhost' IDENTIFIED BY 'mypass' WITH GRANT OPTION;`

Change user password:

`mysql> UPDATE mysql.user SET password=PASSWORD("newpass") WHERE User='username';`

Delete users:

`mysql> DELETE FROM mysql.user WHERE user="username";`

Finally reload the user

```
mysql> FLUSH PRIVILEGES;
mysql> exit;
```

3, Database operations

Show all databases:

`mysql> SHOW DATABASES;`

Create database:

`mysql> CREATE DATABASE mydatabase;`

Use a database:

`mysql> USE mydatabase;`

Delete a database:

`mysql> DROP DATABASE mydatabase;`

Database optimization:
All Databases:
$ sudo mysqlcheck -o --all-databases -u root -p
Single Database:
$ sudo mysqlcheck -o db_schema_name -u root -p

4, Table operations

- Pre-select the database by using the command: mysql> USE mydatabase;

Show entire table:
mysql> SHOW TABLES;

Display table data:
mysql> SELECT * FROM tablename;

Rename table:
mysql> RENAME TABLE first TO second;
or
mysql> ALTER TABLE mytable rename as mynewtable;

Delete table:
mysql> DROP TABLE mytable;

5, Column & row operations

- Pre-select the database by using the command: mysql> USE mydatabase;
Display columns in the table:
mysql> DESC mytable;
or
mysql> SHOW COLUMNS FROM mytable;

Rename columns:
mysql> UPDATE mytable SET mycolumn="newinfo" WHERE mycolumn="oldinfo";

Select data:
mysql> SELECT * FROM mytable WHERE mycolumn='mydata' ORDER BY mycolumn2;

Insert data into the table:
mysql> INSERT INTO mytable VALUES('column1data','column2data','column3data','column4data','column5data','column6data','column7data','column8data','column9data');

Delete data in table:
mysql> DELETE FROM mytable WHERE mycolumn="mydata";

Update data in table:
mysql> UPDATE mytable SET column1="mydata" WHERE column2="mydata";

6, Backup & recovery operations

Back up the entire database with the command (note there is no space between -p and the password):
mysqldump -u root -pmypass --all-databases > alldatabases.sql

Back up any database:
mysqldump -u username -pmypass databasename > database.sql

Restore the entire database with the command:
mysql -u username -pmypass < alldatabases.sql (no space in between -p and mypass)

Restore any database:
mysql -u username -pmypass databasename < database.sql

Backup only database structure:
mysqldump --no-data --databases databasename > structurebackup.sql

Backup multiple database structures only:
mysqldump --no-data --databases databasename1 databasename2 databasename3 > structurebackup.sql

Backup certain tables:
mysqldump --add-drop-table -u username -pmypass databasename table_1 table_2 > databasebackup.sql


**COPYRIGHT : NHANHOA (Copyright © 2002 – 2021 Nhan Hoa Software Company. All Rights Reserved)**
