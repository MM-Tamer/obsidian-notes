Some examples of DDL statements

| Command  | Description                                                                                                          | Syntax                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| CREATE   | Create database or its objects (table, index, function, views, store procedure, and triggers)                        | CREATE TABLE _table_name_ (column1 data_type, column2 data_type, ......); |
| DROP     | Delete objects from the database                                                                                     | DROP TABLE _table_name;                                                   |
| ALTER    | Alter the structure of the  database                                                                                 | ALTER TABLE _table_name_ ADD COLUMN _column_name_ data_type;              |
| TRUNCATE | Remove all records from a table, including all spaces allocated for the records removed (resets the High Water Mark) | TRUNCATE TABLE _table_name_;                                              |
| COMMENT  | Add comments to the data dictionary                                                                                  | COMMENT 'commnet_text' ON TABLE _table_name_;                             |
| RENAME   | Rename an existing object in the database                                                                            | RENAME TABLE _table_name_ TO _new_table_name_;                            |
You can create a table using the structure and the data of another table e.g.:
```sql
CREATE TABLE employees_copy AS SELECT * FROM EMPLOYEES;
```

You can drop columns or modify columns e.g.:

```sql
ALTER TABLE table_name DROP (column1, column2); -- multi column
ALTER TABLE table_name MODIFY (column1_name data_type [DEFAULT 'DEFAULT_VALUE'] [NOT NULL]);

ALTER TABLE table_name DROP COLUMN column_name; -- single column 
```

you can lock a table to be read-only and unlock e.g.:

```sql
ALTER TABLE table_name READ ONLY;
ALTER TABLE table_name READ WRITE;

```

The DROP TABLE statement removes an existing table with all its data from the database and moves it to the recycle bin
After dropping a table, we can restore it for a short time using the FLASHBACK TABLE statement.
After dropping a table, all the objects related to that table will also be deleted or become invalid.
```sql
DROP TABLE table_name;
FLASHBACK TABLE table_name TO BEFORE DROP;
```

| S.NO | DROP                                                                        | TRUNCATE                                                              |
| ---- | --------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| 1.   | The `DROP` command is used to remove the table definition and its contents. | The `TRUNCATE` command is used to delete all the rows from the table. |
| 2.   | In the `DROP` command, table space is freed from memory.                    | The `TRUNCATE` command does not free the table space from memory.     |
| 3.   | `DROP` is a DDL (Data Definition Language) command.                         | `TRUNCATE` is also a DDL (Data Definition Language) command.          |
| 4.   | In the `DROP` command, the view of the table does not exist.                | In the `TRUNCATE` command, the view of the table exists.              |
| 5.   | In the `DROP` command, integrity constraints will be removed.               | In the `TRUNCATE` command, integrity constraints will not be removed. |
| 6.   | In the `DROP` command, undo space is not used.                              | In the `TRUNCATE` command, undo space is used but less than `DELETE`. |
| 7.   | The `DROP` command is quick to perform but gives rise to complications.     | The `TRUNCATE` command is faster than `DROP`.                         |
| 8.   | DROP allows rollback (*if the purge option is not used*)                    | TRUNCATE does not allow rollback                                      |

==RENAME statement:==

The RENAME statement is used to change the name of an existing column or table
We can change the name of a column.
We can change the name of a table.


```sql
ALTER TABLE employee RENAME COLUMN hire_date TO start_date;

ALTER TABLE employee RENAME TO employee_copy;
```


