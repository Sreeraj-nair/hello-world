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

Using Join Queries: Examples 
The following examples show various ways of joining tables in a query. In the first example, an equijoin returns the name and job of each employee and the number and name of the department in which the employee works:

      SELECT last_name, job_id, departments.department_id, department_name
      FROM employees, departments
      WHERE employees.department_id = departments.department_id
      ORDER BY last_name, job_id;
      
      LAST_NAME           JOB_ID     DEPARTMENT_ID DEPARTMENT_NAME
      ------------------- ---------- ------------- ----------------------
         . . .
         Sciarra             FI_ACCOUNT           100 Finance
         Urman               FI_ACCOUNT           100 Finance
         Popp                FI_ACCOUNT           100 Finance
         
         
          . . .
          
       You must use a join to return this data because employee names and jobs are stored in a different table than department names.          Oracle Database combines rows of the two tables according to this join condition:

       employees.department_id = departments.department_id 
      
       The following equijoin returns the name, job, department number, and department name of all sales managers:
   
       SELECT last_name, job_id, departments.department_id, department_name
      FROM employees, departments
      WHERE employees.department_id = departments.department_id
      AND job_id = 'SA_MAN'
      ORDER BY last_name;

      LAST_NAME           JOB_ID     DEPARTMENT_ID DEPARTMENT_NAME
      ------------------- ---------- ------------- -----------------------
      Russell             SA_MAN                80 Sales
      Partners            SA_MAN                80 Sales
      Errazuriz           SA_MAN                80 Sales
      Cambrault           SA_MAN                80 Sales
      Zlotkey             SA_MAN                80 Sales


      This query is identical to the preceding example, except that it uses an additional where_clause condition to return only rows           with a job value of 'SA_MAN'.

Using Subqueries: Examples 
To determine who works in the same department as employee 'Lorentz', issue the following statement:

      SELECT last_name, department_id FROM employees
         WHERE department_id =
           (SELECT department_id FROM employees
            WHERE last_name = 'Lorentz')
         ORDER BY last_name, department_id; 
         
To give all employees in the employees table a 10% raise if they have changed jobs—if they appear in the job_history table—issue the following statement:

      UPDATE employees 
         SET salary = salary * 1.1
         WHERE employee_id IN (SELECT employee_id FROM job_history);
         
To create a second version of the departments table new_departments, with only three of the columns of the original table, issue the following statement:

    CREATE TABLE new_departments 
         (department_id, department_name, location_id)
         AS SELECT department_id, department_name, location_id 
         FROM departments; 

Using Self Joins: Example  
The following query uses a self join to return the name of each employee along with the name of the employee's manager. A WHERE clause is added to shorten the output.

      SELECT e1.last_name||' works for '||e2.last_name 
         "Employees and Their Managers"
         FROM employees e1, employees e2 
         WHERE e1.manager_id = e2.employee_id
            AND e1.last_name LIKE 'R%'
         ORDER BY e1.last_name;

      Employees and Their Managers   
      -------------------------------
      Rajs works for Mourgos
      Raphaely works for King
      Rogers works for Kaufling
      Russell works for King
      
The join condition for this query uses the aliases e1 and e2 for the sample table employees:
         
       e1.manager_id = e2.employee_id

Using Outer Joins: Examples 
The following example shows how a partitioned outer join fills data gaps in rows to facilitate analytic function specification and reliable report formatting. The example first creates a small data table to be used in the join:

      SELECT d.department_id, e.last_name
         FROM departments d LEFT OUTER JOIN employees e
         ON d.department_id = e.department_id
         ORDER BY d.department_id, e.last_name;
         
Users familiar with the traditional Oracle Database outer joins syntax will recognize the same query in this form:

      SELECT d.department_id, e.last_name
         FROM departments d, employees e
         WHERE d.department_id = e.department_id(+)
         ORDER BY d.department_id, e.last_name;
         
 Oracle strongly recommends that you use the more flexible FROM clause join syntax shown in the former example.

The left outer join returns all departments, including those without any employees. The same statement with a right outer join returns all employees, including those not yet assigned to a department:

Note:
The employee Zeuss was added to the employees table for these examples, and is not part of the sample data.

      SELECT d.department_id, e.last_name
         FROM departments d RIGHT OUTER JOIN employees e
         ON d.department_id = e.department_id
         ORDER BY d.department_id, e.last_name;

      DEPARTMENT_ID LAST_NAME
      ------------- -------------------------
      . . .
                110 Higgins
                110 Gietz
                    Grant
                    Zeuss
                    
It is not clear from this result whether employees Grant and Zeuss have department_id NULL, or whether their department_id is not in the departments table. To determine this requires a full outer join:

      SELECT d.department_id as d_dept_id, e.department_id as e_dept_id,
            e.last_name
         FROM departments d FULL OUTER JOIN employees e
         ON d.department_id = e.department_id
         ORDER BY d.department_id, e.last_name;

       D_DEPT_ID  E_DEPT_ID LAST_NAME
      ---------- ---------- -------------------------
        . . .
             110        110 Gietz
             110        110 Higgins
        . . .
             260
             270
                        999 Zeuss
                            Grant

Because the column names in this example are the same in both tables in the join, you can also use the common column feature by specifying the USING clause of the join syntax. The output is the same as for the preceding example except that the USING clause coalesces the two matching columns department_id into a single column output:

      SELECT department_id AS d_e_dept_id, e.last_name
         FROM departments d FULL OUTER JOIN employees e
         USING (department_id)
         ORDER BY department_id, e.last_name;

      D_E_DEPT_ID LAST_NAME
      ----------- -------------------------
        . . .
              110 Higgins
              110 Gietz
        . . .
              260
              270
              999 Zeuss
                  Grant                    

## Using Antijoins
The following example selects a list of employees who are not in a particular set of departments:

      SELECT * FROM employees 
         WHERE department_id NOT IN 
         (SELECT department_id FROM departments 
             WHERE location_id = 1700)
         ORDER BY last_name;

## Using Semijoins: Example 
In the following example, only one row needs to be returned from the departments table, even though many rows in the employees table might match the subquery. If no index has been defined on the salary column in employees, then a semijoin can be used to improve query performance.

      SELECT * FROM departments 
      WHERE EXISTS 
      (SELECT * FROM employees 
          WHERE departments.department_id = employees.department_id 
          AND employees.salary > 2500)
      ORDER BY department_name; 

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
               
     
