# Oracle Error Messages


## SQLWorksheet

### ORA-12541: Cannot connect. No listener at %s

Check for `Listener` status with `lsnrctl status`

If listener is not working start it with:<br>
- `lsnrctl start`
- have to start it as admin. Open comman prompt as admin.
- if trying to start as NOT an admin, will get the error message:
```bash
Unable to OpenSCManager: err=5
TNS-12560: TNS:protocol adapter error
 TNS-00530: Protocol adapter error
```

## Creating Triggers

### ORA-65096: invalid common user or role name

Probably created user in root container where it has no privilages to create Triggers for example.

Create user in PDB container. Do not use root container.

