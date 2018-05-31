---
ID: 6069
post_title: 'TIP: Restore mysql database from idb &#038; frm files.'
post_name: >
  tip-restore-mysql-database-from-idb-frm-files
author: Robbie
post_date: 2017-10-26 13:15:05
layout: post
link: >
  https://xsses.rocks/tip-restore-mysql-database-from-idb-frm-files/
published: true
tags:
  - mysql
  - restore-mysql
categories:
  - Tips
---
The problem : Your server crashed and you recover only the frm and idb files. If you have only the idb files, it works also but you need the SQL scripts with the DB structure.

Copying those files directly in the data directory of a new mysql server will not work. The process is a little bit more complex.

The resolution: It is good to know that table structures are store in .frm files, so the resolution of this problem is to recover those structures, to find the lost data or just recreate the tables. The concept of recovery the structure from a .frm file is really handful because in some cases the MySQL server is not necessary.

Process for recovering one table using .frm files

There are two different ways of recovering corrupted table

Spawning a new MySQL instance and run structure recovery (Usage of the following switches is neede –server or –basedir along with –port)
Recovery of a table without requirement of a MySQL instance (Usage of –diagnostic which reads the .frm files byte-by-byte and tries to recover all the information possible)
First way: Spawning a new MySQL instance and run structure recovery

On ubuntu you will need to run <strong>apt-get install mysql-utilities -y</strong>  to get the tool you need.

Step 1: Recreate the structure from the frm files

To recreate the table structure, you can use the tool “mysqlfrm” provided with MySQL Utilities This tool extracts the structure and create a “Create table” script.
<blockquote> mysqlfrm --user=root --server=root:toor@localhost --port=3111 /root/mysql_table.frm"</blockquote>
The port instruction is any available port, it’s not the port of the mysql server. The end of the script is to redirect the output in a file.

Step 2: Recreate the table in a new database

In a new database, create the new table with the script generated at the step 1.

This script will create 2 files in the database data folder :

mytable.frm
mytable.idb

Step 3: Remove the new idb file

To remove the new idb file, execute the sql command :

ALTER TABLE mytable DISCARD TABLESPACE;

This command removes the link between the table and the tablespace, and removes the idb file.

Step 4: Copy the old idb file

The idb file recovered from the old server must be copied in place of the idb file deleted at the step 3.

Step 5: Reactivate the table

The link broken at the step 3 is restored with the command :

ALTER TABLE mytable IMPORT TABLESPACE;

No worry about the warnings you will receive.

That’s it !

Second way: Recovery of a table without requirement of a MySQL instance

mysqlfrm –diagnostic "&lt;source/path&gt;/mytable.frm" &gt; "&lt;destination/path/recovered_mytable.sql&gt;"

After the execution of the command finishes, all the recovered information for the table will be inside the “recovered_mytable.sql” file.

Steps 2, 3, 4 and 5 from above needs to be repeated in order to idb file be recreated.

Restoring mysql database table from .idb files only

If you have only the idb file from a table, you need the sql script to recreate the tables or at least the corrupted or broken table schema. Skip the step 1 and use the script in the step 2.

Instructions from <a href="http://www.voxteneo.com/restoring-tables-mysql-database-frm-ibd-files-available/">http://www.voxteneo.com/restoring-tables-mysql-database-frm-ibd-files-available/</a>