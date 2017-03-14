Ref https://docs.oracle.com/cd/B28359_01/server.111/b28286/queries006.htm#SQLRF52331

# What are Joins in Oracle? 
A join is a query that combines rows from two or more tables, views, or materialized views. Oracle Database performs a join whenever multiple tables appear in the FROM clause of the query. The select list of the query can select any columns from any of these tables. If any two of these tables have a column name in common, then you must qualify all references to these columns throughout the query with table names to avoid ambiguity.

# Join Conditions 
Most join queries contain at least one join condition, either in the FROM clause or in the WHERE clause. The join condition compares two columns, each from a different table. To execute a join, Oracle Database combines pairs of rows, each containing one row from each table, for which the join condition evaluates to TRUE. The columns in the join conditions need not also appear in the select list.

To execute a join of three or more tables, Oracle first joins two of the tables based on the join conditions comparing their columns and then joins the result to another table based on join conditions containing columns of the joined tables and the new table. Oracle continues this process until all tables are joined into the result. The optimizer determines the order in which Oracle joins tables based on the join conditions, indexes on the tables, and, any available statistics for the tables.

IA WHERE clause that contains a join condition can also contain other conditions that refer to columns of only one table. These conditions can further restrict the rows returned by the join query.

Note:
You cannot specify LOB columns in the WHERE clause if the WHERE clause contains the join condition. The use of LOBs in WHERE clauses is also subject to other restrictions. See Oracle Database SecureFiles and Large Objects Developer's Guide for more information.

# Equijoins 
An equijoin is a join with a join condition containing an equality operator. An equijoin combines rows that have equivalent values for the specified columns. Depending on the internal algorithm the optimizer chooses to execute the join, the total size of the columns in the equijoin condition in a single table may be limited to the size of a data block minus some overhead. The size of a data block is specified by the initialization parameter DB_BLOCK_SIZE.

## Example 
    
    SQL> select * from t1;

        ID
----------
         1
         2
         3
         4

    SQL> select * from t2;

        ID
----------
         3
         4
         5
         6

    -- LEFT OUTER JOIN
    SQL> select t1.id, t2.id from t1 LEFT OUTER JOIN t2 ON (t1.id = t2.id);

        ID         ID
---------- ----------
         3          3
         4          4
         1
         2

    -- RIGHT OUTER JOIN
    SQL> select t1.id, t2.id from t1 RIGHT OUTER JOIN t2 ON (t1.id = t2.id);

        ID         ID
---------- ----------
         3          3
         4          4
                    6
                    5

    -- LEFT JOIN (SAME AS LEFT OUTER JOIN)
    SQL> select t1.id, t2.id from t1 LEFT JOIN t2 ON (t1.id = t2.id)

        ID         ID
---------- ----------
         3          3
         4          4
         1
         2

    -- RIGHT JOIN (SAME AS RIGHT OUTER JOIN)
    SQL> select t1.id, t2.id from t1 RIGHT JOIN t2 ON (t1.id = t2.id)

        ID         ID
---------- ----------
         3          3
         4          4
                    6
                    5

    -- INNER JOIN (REGULAR JOIN)
    SQL> select t1.id, t2.id from t1 INNER JOIN t2 ON (t1.id = t2.id)

        ID         ID
---------- ----------
         3          3
         4          4

    -- FULL OUTER JOIN
    SQL> select t1.id, t2.id from t1 FULL OUTER JOIN t2 ON (t1.id = t2.id)

        ID         ID
---------- ----------
         3          3
         4          4
         1
         2
                    6
                    5

    6 rows selected.

    SQL>
               
     
