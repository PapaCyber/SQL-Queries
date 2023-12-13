# Using SQL queries to filter Data

## Project Description

In this project, a potential security incident occurred after business hours. I examined the organization’s datasets and investigated potential security issues using SQL queries.

### The organization database contains two tables:
- `log_in_attempts`
- `Employees`

### Log_In_Attempts Table

Columns:
- `event_id`: Identification number assigned to each login event
- `username`: Username of the employee
- `login_date`: Date the login attempt was recorded
- `login_time`: Time the login attempt was recorded
- `country`: Country where the login attempt occurred
- `ip_address`: IP address of that employee’s machine
- `success`: Success of the login attempt; FALSE indicates a failed attempt

### Employees Table

Columns:
- `employee_id`: Identification number assigned to each employee
- `device_id`: Identification number assigned to each device used by the employee
- `username`: Username of the employee
- `department`: Department the employee is in
- `office`: The office the employee is located in
# SQL Examples
<details>
<Summary>Cick Here</Summary>
<Br>  
To better understand SQL, here is an explanation of the queries used.

Two SQL queries will always be used to query a SQL dataset: `SELECT` and `FROM`.

For example, if I want to return specific tables like `username` and `department` from the `employees` table:

```
SELECT username, department
FROM employees;
```
When I add a semicolon (`;`) at the end of my query, it tells SQL that is the end of my query.

If I want to return all the columns from the employees table,
I would need to add an asterisk (`*`) after `SELECT`
For example  `SELECT*`

To filter the data I would need to use a third SQL keyword after `FROM` called `WHERE`.

`WHERE` indicates the condition of that filter

If I want to see employees from the finance department
I would type

```
SELECT*
FROM employees
WHERE department = ‘finance’;
```
Instead of using the `WHERE` keyword, I can replace it with `ORDER BY` and pair the keyword with `DESC`, to sort it in descending order.

```
SELECT customerid, city, country
FROM customers
ORDER BY login_time DESC;
```
### Operators
When filtering **numeric** and **data and time data*Z*, it involves **operators**.

Here are the operators that can be used:

| Operator | Use | Example |
| :---         | :---           | :---          |
| `<`  | Less than     | `SELECT`* <br>`FROM` log_in_attempts<br> `WHERE` login_time  `<` ’10:00’; |
| `>`     | Greater than       |    |
| `=`   | Equal to     |   |
| `<=`   | Less than or equal to       |      |
| `>=`   | Greater than or equal to     |     |
| `<>`   | Not equal to     |    |
| `AND`    | `AND` is used to filter on two conditions. `AND` specifies that both conditions must be met simultaneously. You use `AND` after the first condition.     | `SELECT`* <BR>`FROM` log_in_attempts<BR>`WHERE` login_time  `<` ’10:00’ `AND`  login_date `>` '2022-01-09'      |
| `BETWEEN`   | Used for numeric data as well as date and time data is the `BETWEEN` operator. <br>**NOTE**: You use `BETWEEN` after specifying what column you want returned.     | `SELECT`*<br>`FROM` log_in_attempts<br>`WHERE` login_date `BETWEEN` ‘2005-01-01’ `AND` ‘2005-01-02’;    |
| `OR`     | The `OR` operator also connects two conditions, but `OR` specifies that either condition can be met. It returns results where the first condition, the second condition, or both are met. <br>**NOTE**: You use `OR` after the first condition.       | `SELECT`*<Br>`FROM` employees<br>`WHERE` department `=` ‘sales’ `OR` department `=` ‘marketing’;|
| `NOT`     |  The `NOT` operator only works on a single condition, and not on multiple ones. The `NOT` operator negates a condition. <br>**NOTE**: You add this operator after `WHERE`, then put the conditions after it|  `SELECT`*<br>`FROM` log_in_attempts<br>`WHERE` `NOT` login_time  `<` ’10:00’;    |

### Filtering for Patterns
You can also filter based on a pattern. For example, you can identify entries that start or end with a certain character or characters. Filtering for a pattern requires incorporating two more elements into your `WHERE` clause:
- a wildcard 
- the `LIKE` operator

### Wildcards

A wildcard is a special character that can be substituted with any other character. Two of the most useful wildcards are the percentage sign (`%`) and the underscore (`_`):
- The percentage sign substitutes for any number of other characters. 
- The underscore symbol only substitutes for one other character.

These wildcards can be placed after a string, before a string, or in both locations depending on the pattern you’re filtering for.
The following table includes these wildcards applied to the string 'a' and examples of what each pattern would return.

| Pattern     | Results That Could Be Returned |
| :---      | :---       |
| ` 'a%' ` | apple123, art, a         |
| ` 'a_' `     | as, an, a7        |
| ` 'a__' ` | ant, add, a1c         |
| ` '%a' `     | pizza, Z6ra, a        |
| ` '_a' ` | ma, 1a, Ha         |
| ` '%a%' `     | Again, back, a        |
| ` '_a_' `     | Car, ban, ea7        |

### LIKE
To apply wildcards to the filter, you need to use the `LIKE` operator instead of an equals sign (`=`). `LIKE` is used with `WHERE` to search for a pattern in a column. 
For instance, if you want to view the login attempts by the country US, but know that some datasets use USA instead of US, you can use ‘US`%`’ and that will yield a result with the letters “US” for the first 2 letters and any other characters after that.

```
SELECT*
FROM login_attemps
WHERE country LIKE 'us%';
```
This query returns all records with values in the title column that start with the pattern of 'US'. This means both 'US' and 'USA’ are returned.
</details>




