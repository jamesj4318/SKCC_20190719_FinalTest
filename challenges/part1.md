# SK C&C Big Data Knowledge Test
## Part I

### 1. Create a CDH Cluster on AWS
a. Linux setup

i. Add the following linux accounts to all nodes

1. User training with a UID of 3800
2. Set the password for user “training” to “training”
3. Create the group skcc and add training to it
4. Give training sudo capabilities
```
$ sudo useradd training -u 3800
$ sudo passwd training
$ sudo groupadd skcc
$ sudo usermod -a -G skcc training
```

ii. List the your instances by IP address and DNS name (don’t use /etc/hosts
for this)
```
172.31.40.88	nd1.ys.com	nd1
172.31.39.123	nd2.ys.com	nd2
172.31.34.251	nd3.ys.com	nd3
172.31.37.200	nd4.ys.com	nd4
172.31.46.127	nd5.ys.com	nd5
```
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-ii.Instances.PNG?raw=true)

iii. List the Linux release you are using
```
$ cat /etc/redhat-release
```
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-iii.LinuxRelease.PNG?raw=true)

iv. List the file system capacity for the first node (master node)
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-iv.file_system_capacity_for_the_first_node.PNG?raw=true)

v. List the command and output for yum repolist enabled
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-v.yum_repolist.PNG?raw=true)

vi. List the /etc/passwd entries for training (only in master name node)
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-vi.etc_passwd_entries_for_training.PNG?raw=true)

vii. List the /etc/group entries for skcc (only in master name node)
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-vii.etc_group_entries_for_skcc.PNG?raw=true)

viii. List output of the flowing commands:
1. getent group skcc
2. getent passwd training
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-a-viii.getent.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
b. Install a MySQl server

i. Use MariaDB as the database for all the services. You may choose your
own username and passwords but make a record of it so that we may
access them.

ii. List the following in your GitHub
1. A command and output that shows the hostname of your
database server
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-b-ii-1.hostname.PNG?raw=true)
2. A command and output that reports the database server version
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-b-ii-2.dbserver_version.PNG?raw=true)
3. A command and output that lists all the databases in the server
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-b-ii-3.lists_all.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
c. Install Cloudera Manager

i. Specifically, you MUST install CDH version 5.15.2 You will lose points if you install any other version of CDH.

ii. The Cluster does not have to be in HA mode.

iii. Make sure that the following services (and any necessary services to install that service) are installed:
1. HDFS
2. YARN
3. Sqoop
4. Hive
5. Impala
6. HUE

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-c-iii.makesure_services.PNG?raw=true)

iv. In you cluster, create a user named “training” with password “training”
1. You should have already created the linux user from previous step. Now, make sure user “training” has both a linux and HDFS home directory

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/1-c-iv.create_user_training.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
2. In MySQL create the sample tables that will be used for the rest of the test
a. In MySQL, create a database and name it “test”

![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/2-a.create_db_test.PNG?raw=true)

b. Create 2 tables in the test databases: authors and posts.
i. You will use the authors.sql and posts.sql script files that will be provided for you to generate the necessary tables
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/2-b.create_2_tables.PNG?raw=true)

c. Create and grant user “training” with password “training” full access to the test database. (It is ok if you give training full access to the entire MySQL database)
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/2-c.1.PNG?raw=true)
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/2-c.2.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
3. Extract tables authors and posts from the database and create Hive tables.

a. Use Sqoop to import the data from authors and posts

b. For both tables, you will import the data in tab delimited text format

c. The imported data should be saved in training’s HDFS home directory

i. Create authors and posts directories in your HDFS home directory

ii. Save the imported data in each

d. In Hive, create 2 tables: authors and posts. They will contain the data that you
imported from Sqoop in above step.

e. You are free to use whatever database in Hive.

f. Create authors as an external table.

g. Create posts as a managed table.
```
sqoop import --connect jdbc:mysql://172.31.40.88/test --username training --password training --table authors --target-dir /user/hive/warehouse/authors --hive-import --create-hive-table --hive-table default.authors
```
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/3-1.PNG?raw=true)

```
sqoop import --connect jdbc:mysql://172.31.40.88/test --username training --password training --table posts --target-dir /user/hive/warehouse/posts --hive-import --create-hive-table --hive-table default.posts
```
![photo.PNG](https://github.com/jamesj4318/SKCC_20190719_FinalTest/blob/master/challenges/images/3-2.PNG?raw=true)

----------------------------------------------------------------------------------------------------------------------------------------
4. Create and run a Hive/Impala query. From the query, generate the results dataset that you will use in the next step to export in MySQL.






