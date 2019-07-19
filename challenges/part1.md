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

iii. List the Linux release you are using
```
$ cat /etc/redhat-release
```


iv. List the file system capacity for the first node (master node)

v. List the command and output for yum repolist enabled

vi. List the /etc/passwd entries for training (only in master name node)

vii. List the /etc/group entries for skcc (only in master name node)

viii. List output of the flowing commands:
1. getent group skcc
2. getent passwd training
