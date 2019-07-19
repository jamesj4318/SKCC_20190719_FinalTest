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
iii. List the Linux release you are using
iv. List the file system capacity for the first node (master node)
v. List the command and output for yum repolist enabled
vi. List the /etc/passwd entries for training (only in master name node)
vii. List the /etc/group entries for skcc (only in master name node)
viii. List output of the flowing commands:
1. getent group skcc
2. getent passwd training
