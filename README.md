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
<img src="https://imgur.com/tlAOG2Q.png" height="80%" width="80%"/>

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
<img src="https://imgur.com/DuC6z8n.png" height="80%" width="80%"/>

Instead of using the `WHERE` keyword, I can replace it with `ORDER BY` and pair the keyword with `DESC`, to sort it in descending order.

```
SELECT customerid, city, country
FROM customers
ORDER BY login_time DESC;
```
<img src="https://imgur.com/eNgWu27.png" height="80%" width="80%"/>

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
<img src="https://imgur.com/yu2VeC7.png" height="80%" width="80%"/>

This query returns all records with values in the title column that start with the pattern of 'US'. This means both 'US' and 'USA’ are returned.
</details>

# Retrieve failed login attempts
The potential security event occurred after 18:00 hours.

To investigate I typed this SQL query
```
SELECT* 
FROM log_in_attempts
WHERE login_time > ‘18:00’ AND success = 0;
```
<img src="https://imgur.com/YUuCfdX.png" height="80%" width="80%"/>

| I discovered that there were 19 failed attempts after 18:00     |
| :---      |

I filtered the failed login attempts after 18:00 hours, by using the great than sign (`>`).


1 = success
<Br>0 = failed

**Note**: we don’t add quotations (‘ ‘) to plain numbers, but when it comes to date and time we have to add quotations between them.


# Retrieve login attempts on specific dates
A suspicious event on 2022-05-09 or 2022-05-08. 

I used the SQL query
```
SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```
I used the `OR` operator to get data from either of the dates 2022-05-09 or 2022-05-08. I used the equals (`=`) to get the exact dates that I wanted.

<img src="https://imgur.com/ysQK8zp.png" height="80%" width="80%"/>

| There were 75 login attempts between the two days.   |
| :---      |

# Retrieve login attempts outside of Mexico
The team is investigating logins that did not originate in Mexico.

I used the SQL query
```
SELECT * 
FROM log_in_attempts 
WHERE NOT country LIKE 'MEX%';
```
I used the `NOT` operator to filter out MEXICO from the results. Since MEXICO can be spelled like “MEX” or “MEXICO”. I had to use the `LIKE` operator along with a wildcard which is the percentage sign (`%`) to remove any country spelled with MEX at the beginning. 

<img src="https://imgur.com/Asc73nu.png" height="80%" width="80%"/>

| There were 144 login attempts were outside of Mexico.   |
| :---      |

# Retrieve employees in Marketing
I was given the task of retrieving all the employees from the marketing department who were from all the offices in the east building.

I used the SQL query
```
Select*
FROM employees
WHERE department = ‘marketing’ AND office LIKE ‘East%’;
```

Similar to the previous SQL query I used a wildcard, percent (`%`) for office buildings that had the word East in them. I combined the two conditions with the `AND` operator to find all marketing employees from the east office.

<img src="https://imgur.com/L6lgs60.png" height="80%" width="80%"/>

| There are 7 employees from the marketing department that work in the east buildings.    |
| :---      |

# Retrieve employees in Finance or Sales
The team needs to perform different updates to the computers of all employees in the Finance or the Sales department, so I need to locate information on these employees.

I used the SQL query
```
SELECT*
FROM employees
WHERE department = ‘finance’ OR department = ‘sales’;
```
<img src="https://imgur.com/tAG7ufx.png" height="80%" width="80%"/>

| I found that 71 employee's computers in Finance and Sales department need updates.   |
| :---      |

# Retrieve all employees not in IT
Our team needs to make one more update. Since the Information Technology department already received updates. I need to retrieve information from all the other departments.

I used the SQL query
```
SELECT*
FROM employees
WHERE NOT department = ‘Information Technology’;
```
To remove the Information Technology department from the results I used the `NOT` keyword after `WHERE`.

<img src="https://imgur.com/ATG06So.png" height="80%" width="80%"/>

| 161 employee’s computers that were not in the IT department need updates.    |
| :---      |

# Summary
At the end of this project, I discovered how powerful SQL queries are. Instead of using GUI to retrieve this information, CLI is much more efficient in retrieving data that is needed for a typical security professional. 






