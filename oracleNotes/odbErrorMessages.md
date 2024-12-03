# Oracle Error Messages

## Creating Triggers

### ORA-65096: invalid common user or role name

Probably created user in root container where it has no privilages to create Triggers for example.

Create user in PDB container. Do not use root container.

