Getting Started with MySQL

## Environment

This environment is a Windows 11 Desktop, using WSL 2 Linux, Ubuntu.

## Update Linux System

    sudo apt-get update

## Upgrade Linux System

    sudo apt-get upgrade

## Installing MySQL from the command line

    sudo apt install mysql-client-core-8.0

    sudo apt-get install mysql-server

## Check the server

The server should have started auto from install to check status of server

    systemctl status mysql

    ● mysql.service - MySQL Community Server
        Loaded: loaded (/usr/lib/systemd/system/mysql.service; enabled; pr>
        Active: active (running) since Thu 2025-08-28 17:34:08 PDT; 57s ago
        Docs: man:mysqld(8)
                http://dev.mysql.com/doc/refman/en/using-systemd.html
    Main PID: 7989 (mysqld)
        Status: "Server is operational"
        Tasks: 38 (limit: 37986)
        Memory: 352.5M (peak: 378.0M)
            CPU: 685ms
        CGroup: /system.slice/mysql.service
                └─7989 /usr/sbin/mysqld

## If the server needs to be restarted

    sudo systemctl start mysql

## Connecting to mysql server with mysql client

    mysql -u root -p

## To disconnect from the mysql server

    quit

## Basic Operations with MySQL

Showing existing databases

    SHOW DATABASES;

    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    +--------------------+

Create a new database

    CREATE DATABASE nameofdatabase;

Create a table inside a database

First pick the database in which you want to create the table with 

    USE

Statement

    USE test;

Create a table statement

    CREATE TABLE tableOne
    (

        id  INT unsigned NOT NULL AUTO_INCREMENT,
        name VARCHAR(150) NOT NULL,
        owner VARCHAR(150) NOT NULL,
        PRIMARY KEY (id)

    );

Show table

    SHOW TABLES;

    +----------------+
    | Tables_in_test |
    +----------------+
    | tableOne       |
    +----------------+

Describe shows information on all columns of a table

    DESCRIBE tableOne;

    +-------+--------------+------+-----+---------+----------------+
    | Field | Type         | Null | Key | Default | Extra          |
    +-------+--------------+------+-----+---------+----------------+
    | id    | int unsigned | NO   | PRI | NULL    | auto_increment |
    | name  | varchar(150) | NO   |     | NULL    |                |
    | owner | varchar(150) | NO   |     | NULL    |                |
    +-------+--------------+------+-----+---------+----------------+

Adding records into a table

    INSERT INTO tableOne ( name, owner ) VALUES
    ( 'EchoOne', 'Lennon' ),
    ( 'EchoTwo', 'Casey' ),
    ( 'EchoThree', 'River' );

Retrieving records from a table

    SELECT * FROM tableOne;

    +----+-----------+--------+
    | id | name      | owner  |
    +----+-----------+--------+
    |  1 | EchoOne   | Lennon |
    |  2 | EchoTwo   | Casey  |
    |  3 | EchoThree | River  |
    +----+-----------+--------+

Select specific colums and rows 

    SELECT name FROM tableOne WHERE owner = 'Casey';

    +---------+
    | name    |
    +---------+
    | EchoTwo |
    +---------+

Delete a record from a table

    DELETE FROM tableOne WHERE name='EchoTwo';

Adding or deleting a column a table

    ALTER TABLE tableOne ADD gender CHAR(1) AFTER name;

check to see tables with the DESCRIBE command

    DESCRIBE tableOne;

    +--------+--------------+------+-----+---------+----------------+
    | Field  | Type         | Null | Key | Default | Extra          |
    +--------+--------------+------+-----+---------+----------------+
    | id     | int unsigned | NO   | PRI | NULL    | auto_increment |
    | name   | varchar(150) | NO   |     | NULL    |                |
    | gender | char(1)      | YES  |     | NULL    |                |
    | owner  | varchar(150) | NO   |     | NULL    |                |
    +--------+--------------+------+-----+---------+----------------+

SHOW CREATE TABLE shows a CREATE TABLE statement, which provides even more details on the table:

    SHOW CREATE TABLE tableOne\G

    *************************** 1. row ***************************
        Table: tableOne
    Create Table: CREATE TABLE `tableOne` (
    `id` int unsigned NOT NULL AUTO_INCREMENT,
    `name` varchar(150) NOT NULL,
    `gender` char(1) DEFAULT NULL,
    `owner` varchar(150) NOT NULL,
    PRIMARY KEY (`id`)
    ) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
    1 row in set (0.00 sec)

Use ALTER TABLE...DROP to delete a column:

    ALTER TABLE tableOne DROP gender;

    DESCRIBE tableOne;

    +-------+--------------+------+-----+---------+----------------+
    | Field | Type         | Null | Key | Default | Extra          |
    +-------+--------------+------+-----+---------+----------------+
    | id    | int unsigned | NO   | PRI | NULL    | auto_increment |
    | name  | varchar(150) | NO   |     | NULL    |                |
    | owner | varchar(150) | NO   |     | NULL    |                |
    +-------+--------------+------+-----+---------+----------------+