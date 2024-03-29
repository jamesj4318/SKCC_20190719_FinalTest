# SK C&C Big Data Knowledge Test
## Part II

### 1.

### Instructions

Write a query to compare each active account’s balance to the average balance of all closed accounts of the same type.

### Data Description

The account data exists in the metastore account table in the problem1 database. The amount column gives the account balance. The type column gives the type of account and the status column gives the status of the account.

```
SELECT A.id AS id,
       A.type AS type,
       A.status AS status,
       A.amount AS amount,
       (A.amount-B.avg_amt) AS difference
  FROM account A
  JOIN ( SELECT type ,
                AVG(amount) AS avg_amt
           FROM problem1.account
          GROUP BY type
       ) B
    ON A.type = B.type
 WHERE A.status='Active'
 ```
 
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-1-result.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 2.

### Instructions

Create an employee table in the metastore that contains the employee records stored in HDFS.

### Data Description
All of the employee records are stored in the /user/training/problem2/data/employee/ HDFS directory in Parquet file format.
The files contain the following columns and types:

```
CREATE DATABASE problem2;
```

```
CREATE EXTERNAL TABLE solution
(
    id INT,
    fname STRING,
    lname STRING,
    address STRING,
    city STRING,
    state STRING,
    zip STRING,
    birthday STRING,
    hireday STRING
)
    STORED AS PARQUET
    LOCATION '/user/training/problem2/data/employee'
```

Sample Output:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-2.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 3.

### Instructions

Generate a table that contains all customers who have positive account balances.

### Data Description

The customer records are stored in the customer table in the problem3 database. The account records are stored in the account table in the problem3 database. The account records contain a field called amount that may be negative. The custid field is a foreign key into the customer table.

```
CREATE TABLE solution3 AS
SELECT C.id, C.fname, C.lname, C.hphone
  FROM CUSTOMER C
  JOIN ACCOUNT A
    ON C.id = A.custid
 WHERE A.amount > 0;
```

Sample Output:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-3.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 4.

### Instructions

LoudAcre Mobile has merged with another company located in California. Each company has a list of customers in different formats. Combine the two customer lists into a single dataset using an identical schema.

### Data Description
The original customer data exists in the HDFS directory /user/training/problem4/data/employee1/. It contains expanded, nine-digit zip codes. The new files are in the HDFS directory /user/training/problem4/data/employee2/. It contains last names before first names, both using all capital letters.

----------------------------------------------------------------------------------------------------------------------------------------
### 5.

### Instructions

The bank is making a Facebook group for the Palo Alto, CA branch. Generate a script that outputs the customers and employees who live in Palo Alto, CA.

### Data Description

The employee records are stored in the employee metastore table in the problem5 database, The customer records are stored in the customer metastore table in the problem5 database.

```
SELECT C.fname, C.lname, C.city, C.state
  FROM customer C
 WHERE C.city = 'Palo Alto'
   AND C.state = 'CA'
 UNION ALL
SELECT E.fname, E.lname, E.city, E.state
  FROM employee E
 WHERE E.city = 'Palo Alto'
   AND E.state = 'CA'
```

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-5.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 6.

### Instructions

There are privacy concerns about the employee data that is stored on the cluster. Your task is to remove part of the age information from the employee data by creating a new table for the data analysts to query against.

### Data Description
All of the employee records are stored in the employee metastore table in the problem6 database.

Create Table solutoin:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-6-1.PNG?raw=true)

Change Column Name:
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-6-2.PNG?raw=true)

```
INSERT INTO TABLE problem6.solution
SELECT id, fname, lname, address, city, state, zip, substring(birthday, 7 ,10)
  FROM problem6.employee
```

Sample Output:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-6-result.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 7.

### Instructions

Generate a report that contains all of the Seattle employee names in sorted order.

### Data Description

The employee records are stored in the employee table in the problem7 database.

```
SELECT CONCAT(lname, ', ' , fname) AS name
  FROM employee
 WHERE city = 'Seattle'
 ORDER BY name
```

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-7-result.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 8.

### Instructions

Use Sqoop to export customer data from HDFS into a MySQL database table. Place the data in the solution table in MySQL, which has been created and is currently empty.

### Data Description

The data files are in the HDFS directory /user/training/problem8/data/customer/.

MySQL database information:

 Installation: localhost

 Database name: problem8

 Table name: solution

 Username: cloudera

 Password: cloudera

```
sqoop export --connect jdbc:mysql://localhost/problem8 --username cloudera --password cloudera --export-dir /user/training/problem8/data/customer --table solution --input-fields-terminated-by '\t'
```

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-8-1.PNG?raw=true)


----------------------------------------------------------------------------------------------------------------------------------------
### 9.

### Instructions

Your company is being acquired by another company. To prepare for this acquisition, update the customer records to guarantee there will be no duplicate IDs with their existing customer IDs.

### Data Description

The customer records are stored in the customer table in the problem9 database. The id column is a unique identifier for that record.

Create Table solution:

```
CREATE TABLE solution
(
	  id STRING,
	  fname STRING,
	  lname STRING,
	  address STRING,
	  city STRING,
	  state STRING,
	  zip STRING,
	  birthday STRING
)
```

Insert Into:

```
INSERT INTO TABLE solution
SELECT CONCAT('A', id),
	     fname,
	     lname,
	     address,
	     city,
	     state,
	     zip,
	     birthday
  FROM customer;
```

Sample Output:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-9-result.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
### 10.

### Instructions

Your boss needs specialized reports using the billing data and is constantly asking for help to write SQL queries. Create a database view in the metastore so that your boss has customer and billing data joined.

### Data Description

The customer data exists in the customer metastore table in the problem10 database.
The billing data exists in the billing metastore table in the problem10 database. The id column is a foreign key into which customer has the charge.

Create New View:

```
CREATE VIEW solution AS
SELECT C.id AS id,
       C.fname AS fname,
       C.lname AS lname,
       C.state AS state,
       C.zip AS zipcode,
       B.charge AS charge,
       substr(B.tstamp,1,10) AS billdate
  FROM customer C
  JOIN billing B
    ON C.id = B.id;
```

Output:

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-10-result.PNG?raw=true)


