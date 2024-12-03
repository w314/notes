# SQL Developer

## Connect to DB
- Click `+` icon to add db connection

DO NOT connect to root container. 
- use username that you created NOT SYS
- Use `Service name: XEDB1` (not SID: xe)


`XEDB1` is an oracle XE provided pluggable database.



## Errors

### Error when opening sql developer: `Warning - could not install some modules:`

To solve:
- go to:
- `C:\Users\<YOUR_USERNAME>\AppData\Roaming\SQL Developer\system<YOUR_SQLDEVELOPER_VERSION>\system_cache\config\Modules`
- delete whatever exists in that folder

## Error when tyring to open worksheet
> ORA-12541: Cannot connect. No listener at %s

Reason: the listener is not working you can check the status with `lsnrctl status`

If listener is not working start it with:<br>
- `lsnrctl start`
- HAVE to run it as admin Open command prompt as admin.
- if trying to start as NOT an admin, will get the error message:
```bash
Unable to OpenSCManager: err=5
TNS-12560: TNS:protocol adapter error
 TNS-00530: Protocol adapter error
```

With OracleServiceXE running.



## Tricks

### How to turn on code line numbers

[Source](https://www.databasestar.com/sql-developer-line-numbers/)

Tools > Preferences > Code Editor > Line Gutter > Show Line Numbers

### ShortCuts

- `ALT+F10` new worksheet
- `CTRL+SPACE` list columns of a table when table after `<table_name>.`
- `F5` run query

