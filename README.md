# Apply filters to SQL queries project

Hands on Lab for filtering SQL queries done for the Google Cybersecurity course. This was a project that connected a series of SQL labs to an ongoing Incident Journal project. 

## Project description

  <Details Open><Summary>
    
  ### Goal

  </Summary>

  - Use SQL to search login times and locations in a database
  
  - Use SQL to find failed login attempts
  
  - Apply the WHERE clause to filter what a SQL query returns and
  
  - use the LIKE operator to filter for patterns.

  
  </Details>
  
  <Details Open><Summary>
    
  ### Scenario

  </Summary>
  
  > "My organization is working to make their system more secure. It is my job to ensure the system is safe, investigate all potential security issues, and update employee computers as needed. The following steps provide examples of how I used SQL with    
  filters to perform security-related tasks."

  </Details>

  <Details Open><Summary>
    
  ### Code/Commands

  </Summary>

  - SQL
    - (Specific commands will be explained in the 'Tasks' Sections)   

  - Bash

  </Details>

  <Details Open><Summary>
    
  ### Environment
  
  </Summary>
  
  - Linux on Virtual machine provided by QwikLabs 
  - MariaDB
  
  </Details>
  
## Task1 Retrieve after hours failed login attempts

> "There was a potential security incident that occurred after business hours (after 18:00). All after hours login attempts that failed need to be investigated."

The following code is the query I used to return events that match the investigation parameters.

<Details Open><Summary><h3>SQL Query</h3></Summary>
    
```SQL
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;
```
<img width="900" alt="sql1ab" src="https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/9c07fdf3-0350-43e9-a4b6-dc9258971c0a">

Returned 19 login attempts that failed.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

My query filters for failed login attempts that occured after 18:00. 

`SELECT *` - Select all data `*` indicates all data or a wildcard.

`FROM log_in_attempts` - Indicates where all the data should be selected form, the `log_in_attempts` table.

`WHERE` - Clause used to filter output in this case login time after 18:00.

`AND` - Operator used to connect two condition, both conditions must be met simultaneously, in this case login time and failed login success.

``login_time > `18:00`` - First Condition used to select logins after 18:00 

`success = FALSE` - Second condition, failed logins. 
 
</Details>

## Task 2 Retrieve login attempts on specific dates
 
> "A suspicious event occurred on 2022-05-09. Any login activity that happened on 2022-05-09 or on the day before needs to be investigated."

This is the SQL query I used to filter for login attempts that occurred on specific dates.

<Details Open><Summary><h3>SQL Query</h3></Summary>
  
```SQL
SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```
![SQL2ab](https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/20c0d331-cb1b-4c95-baf8-198d093e4f55)

Returned 76 login attempts during those dates.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

`SELECT *`
`FROM log_in_attempts` -  Select all data in the `log_in_attempts` table.

`WHERE` - Clause that indicates the condition for a filter.

`OR` - operator that specifies either condition can be met in a filter that contains two conditions, in this case either dates conditioned.

`login_date = '2022-05-09' OR login_date = '2022-05-08'` - dates to filter logins by.

</Details>

## Task 3 Retrieve login attempts outside of Mexico

> "After investigating the organization’s data on login attempts, I believe there is an issue with the login attempts that occurred outside of Mexico. These login attempts should be investigated."

The following code is what I used to filter login attempts that occured outside of Mexico.

<Details Open><Summary><h3>SQL Query</h3></Summary>

```SQL
SELECT * 
FROM log_in_attempts 
WHERE NOT country LIKE 'MEX%';
```
![SQL3ab](https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/0fb78499-86a2-4710-a67b-84d2ca65d606)

There were 144 login attempts that occured outside of Mexico.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

`SELECT *`
`FROM log_in_attempts` - Same as above.

`WHERE` - Indicates the condition for a filter.

`NOT` - Used to negate a condition, in this case countries other than Mexico.

`LIKE` - Used with  `WHERE` to search for a pattern in a column. I used it with `MEX%` as the pattern to match.

`%` - Represents any number of unspecified characters when used with `LIKE`. Allowing for `MEX%` to return `MEX` and `MEXICO`.

</Details>

## Task 4 Retrieve employees in Marketing

> "My team wants to update the computers for certain employees in the Marketing department. To do this, I have to get information on which employee machines to update."

This is the SQL query I used to filter employee machines from employees in the Marketing department in the East building.

<Details Open><Summary><h3>SQL Query</h3></Summary>
  
```SQL
SELECT * 
FROM employees 
WHERE department = 'Marketing' AND office LIKE 'East%';
```
<img width="900" alt="SQL4ab" src="https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/c631bcfa-18ab-415a-af07-5741ab708a7e">

The query returned 7 machines to update.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

This query returns all employees in the Marketing department in the East building. 

`SELECT *`
`FROM employees` - Select all data from the `employees` table.

``Where department = `Marketing`` - First condition indicating to return data from 'Marketing' department connected to second condition with `AND`. 

``AND office LIKE `East%`` - `AND` is used to connect both "department" and "office" to filter for employees. `%` is used with "East" to represent unspecified characters, in this case east offices.  

</Details>

## Task 5 Retrieve employees in Finance or Sales

> "The machines for employees in the Finance and Sales departments also need to be updated. Since a different security update is needed, I have to get information on employees only from these two departments."

This is the SQL query I used to filter for employee machines from employees in the Finance or Sales departments.

<Details Open><Summary><h3>SQL Query</h3></Summary>
  
```SQL
SELECT * 
FROM employees 
WHERE department = 'Finance' OR department = 'Sales';
```
![SQL5ab](https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/89705f44-4568-41d6-9c81-97b8fbd6506a)

Query returns 71 employees that fit the parameters.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

First part of this query selects all data from the `employees` table. `WHERE` clause with `OR` is used to filter for employees who are in the Finance and Sales departments.

`OR` - Operator, specifies that either condition can be met, I used it instead of `AND` because I want employees in either department
  
`department = 'Finance'` `department = 'Sales'` Each condition filters which departments I am looking for data in, `OR` connects them and specifies returns from either.

</Details>

## Task 6 Retrieve all employees not in IT

> "My team needs to make one more security update on employees who are not in the Information Technology department. To make the update, I first have to get information on these employees."

This is the SQL query I used to filter the employees not in the IT department.

<Details Open><Summary><h3>SQL Query</h3></Summary>
  
```SQL
SELECT * 
FROM employees 
WHERE NOT department = 'Information Technology';
```
![SQL6ab](https://github.com/JustinRoberg/FilterSQLQueries/assets/133618188/c34d3883-7c3d-43f9-aa64-9c3edd6fcd9e)

Returns 161 employees not in IT department.

</Details>

<Details Open><Summary><h3>Explanation</h3></Summary>

First I selected all data from the `employees` table, then used the `WHERE` clause with the `NOT` filter.

``NOT department = `Information Technology`` - I used `NOT` to filter out the department "Information Technology" to return all other departments.

`=` - Used in filters to return only the records that contain a value in a specified column that is equal to a particular value

</Details>

## Summary

I used SQL queries to get data and information on specific login attempts and employee machines needing updates. Used two tables and several operators to filter the information.

[Additional SQL Reference notes](https://docs.google.com/document/d/1QVfrtp4QywbvQ5ALupN7-gKNrXI9yrYDv6PyCwWVAYg) 


