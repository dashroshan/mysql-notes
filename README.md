# Setup and run

## Start-stop mysql server

```sql
-- Run cmd as administrator
net start mysql80 -- Start server
net stop mysql80 -- Stop server
mysql -u 'username' -p -- Open mysql, Account: root, pass
```

## Create new user

```sql
-- Create user
create user 'username' identified by 'password';

-- Modify user
alter user 'username' identified by 'newpassword';

-- Grant all permisions on all databases and tables
grant all on *.* to 'username' with grant option;
```

# Basic Operations

## Database

```sql
show databases; -- Show all db names
create database database_name; -- Create
drop database database_name; -- Delete
use database_name; -- Select to use
```

## Table

```sql
show tables; -- Show all table names
create table table_name(
    column_name1 type_1 args_1,
    column_name2 type_2 args_2,
    ...
); -- Create
drop table table_name; -- Delete
describe table_name; -- Show columns of table
```

## Add records to table

```sql
-- Values must be given in the same column order as the table.
-- All columns must be given a value.
insert into table_name values
(col1_value1, col2_value1, ... ),
...
(col1_valueN, col2_valueN, ... );

-- Values given in the column order specified by us in the query.
-- Optional columns can be ignored.
insert into table_name
(col1, col2, ... )
values
(col1_value1, col2_value1, ... ),
...
(col1_valueN, col2_valueN, ... );
```

# Select records

## Structure

```sql
select <expression> -- required
from <structure(s)> -- required
where <clause> -- optional
group by <clause> -- optional
having <clause> -- optional
order by <clause>; -- optional
```

## Select

What to display

```sql
select * -- all columns
select col1, col2 -- column 1 and 2 only
select distinct col1 -- distinct records by column 1 only
select distinct col1, col2 -- distinct record by combination of column 1 and 2

select originalColName as newColName -- Change the displayed table heading name
select cost * 5 -- +, -, *, / can be used
select concat(col1, " hi ", col2) -- "col1_data hi col2_data"
select myDate + interval 1 day as dayAfter -- day, hour, minute, month, year etc available
```

## From

What raw data to select from

```sql
from tablename
```

## Where

Filter data from the raw data where a condition is matched

```sql
where condn1 <and/or/&&/||> condn2 ... condn
-- we can use brackets like: c1 and (c2 or c3)
```

Condition examples

```sql
id = 3 -- Similarly we can use <, >, <=, >=
id * 2 = 6 -- +, -, *, / can be used
not city = "Puri" -- Way 1 to do NOT
city <> "Puri" -- Way 2 to do NOT
city != "Puri" -- Way 3 to do NOT
id in (2,3,4,5)
exists (select * from anotherTable where anotherTable.id = mainTable.id) -- True if the subquery has a result
name like "_u%t" -- _ match single char and % match multiple chars, this will match 'Punit', 'Suit' etc. Also works with numbers.
id between 3 and 5 -- Both values included
```
