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
2. A command and output that reports the database server version
3. A command and output that lists all the databases in the server








