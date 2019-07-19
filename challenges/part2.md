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




