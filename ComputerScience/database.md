# 1 relational database(mysql)
## 1.1 数据类型

## 1.2 建立表格
```sql
  CREATE TABLE person
     (person_id SMALLINT UNSIGNED,
      fname VARCHAR(20),
      lname VARCHAR(20),
      eye_color CHAR(2),
      birth_date DATE,
      street VARCHAR(30),
      city VARCHAR(20),
      state VARCHAR(20),
      country VARCHAR(20),
      postal_code VARCHAR(20),
      CONSTRAINT pk_person PRIMARY KEY (person_id)

);
```

### 1.2.1 constain
primary key:

allowable value:

foreign key

## 1.3 数据操作
![[Screen Shot 2022-10-28 at 16.35.38.png]]
### 1.3.1 SELECT
``` sql
SELECT select_list
FROM table_name;
```
typical : select * / columns(use , seperate)

use the MySQL `SELECT` statement without referencing any table.
MySQL has many built-in functions like string, date, and Math functions. And you can use the `SELECT` statement to execute these functions.

The following example returns the current date and time of the MySQL server:
```sql
mysql> select NOW();

+---------------------+

| NOW()               |

+---------------------+

| 2022-10-28 15:56:43 |

+---------------------+

1 row in set (0.00 sec)
```

```sql
SELECT expression AS column_alias; //alias of expression
```

### 1.3.2 order by
```sql
SELECT   firstName,lastName,      officeCode 
FROM      employees 
WHERE     officeCode IN (1 , 2, 3) 
ORDER BY  officeCode DESC;//default asc
```

### 1.3.3 join
A join is a method of linking data between one ([self-join](http://www.mysqltutorial.org/mysql-self-join/)) or more tables based on values of the common column between the tables.

```sql
select CONCAT(lastName, firstName) AS name, offices.city 
from employees 
inner join offices using(officeCode);

+------------------+---------------+
| name             | city          |
+------------------+---------------+
| MurphyDiane      | San Francisco |
| PattersonMary    | San Francisco |
| FirrelliJeff     | San Francisco |
| BowAnthony       | San Francisco |
| JenningsLeslie   | San Francisco |
| ThompsonLeslie   | San Francisco |
| FirrelliJulie    | Boston        |
| PattersonSteve   | Boston        |
| TsengFoon Yue    | NYC           |
| VanaufGeorge     | NYC           |
+------------------+---------------+
```

# 2 nosql:
cassandra