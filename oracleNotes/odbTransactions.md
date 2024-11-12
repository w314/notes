# Oracle Transaction Processing

- transaction processing allows multiple user to work on the same database
- Oracle uses locks to control concurrent access
- Oracle locks only the minimuml amount of data for the least possible time


## Transaction Processing Commands

- `COMMIT`
    - makes the changes in the current transaction permanent in the database
    - changes made are also visible to others
- `ROLLBACK`
    - restors the state of the sdatabase (undoes changes) 
        - to a `savepoint`
        - or to the last commit point
- `SAVEPOINT`
    - used to mark and name a current point in the transaction
    - makes it possible to undo/rollback part of a transaction 