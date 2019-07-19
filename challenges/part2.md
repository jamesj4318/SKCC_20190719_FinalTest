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

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/part2-6-result.PNG?raw=true)
















