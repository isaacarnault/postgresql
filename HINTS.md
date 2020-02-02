Useful PostgreSQL Linux commands

#### Checking the service status
```r
$ ubuntu@ipv4-public-address:~$ systemctl status postgresql.service
$ ubuntu@ipv4-public-address:~$ systemctl status postgresql@12-main.service
$ ubuntu@ipv4-public-address:~$ systemctl status postgresql@12-main.service
```
#### Troubleshooting
If pgAdmin 4 does not launch on your web browser :<br>
<b>Way to check if you receive traffic to your EC2 vm</b><br>
Open a new Terminal window (Ctrl + Alt + T) and ping your EC2 instance's IPV4 public address : <br>
If you receive some packets, this mean your VM is accepting traffic.<br>
Please note that traffic restrictions on `AWS` may be caused by improper Security Group configuration: your EC2 instance should at least allow inbound traffic on port 22 (SSH) and outbound traffic on Http and Https.

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-20.png](https://i.postimg.cc/zG7BqChP/isaac-arnault-aws-20.png)](https://postimg.cc/5XH13Fnw)

</p>
</details>

#### Useful syntax
<b>Create a user</b>
```r
mydatabase=# CREATE USER zaki WITH SUPERUSER LOGIN PASSWORD 'mypassword';
```
<b>Check whether the user has been created or not</b>
```r
mydatabase=# \du
```
<b>Log in with the user “zaki”</b>
```r
postgres@ip-v4-address:~$ psql su -l zaki
# OR
postgres@ip-v4-address:~$ psql -h localhost -d test -U zaki
```
<b>Delete a user</b>
```r
postgres@ip-v4-address:~$ sudo deluser zaki
```
<b>List all databases</b>
```r
mydatabase=# \l
```
<b>Logout from your database</b>
```r
mydatabase=# \q
```
<b>Logout from user "postgres"</b>
```r
postgres@ipv4-public-address:~$ exit
```
<b>List all `PostgreSQL` packages</b>
```r
ubuntu@ipv4-public-address:~$ pdpkg -l | grep postgres
```
<b>Delete all `PostgreSQL` packages</b>
```r
ubuntu@ipv4-public-address:~$ apt-get --purge remove package1 package2 packagen
```
<b>Verify that all `PostgreSQL` packages are deleted</b>
```r
ubuntu@ipv4-public-address:~$ pdpkg -l | grep postgres
```
<b>Remove `PostgreSQL` from your `EC2` compute machine or `Linux` virtual machine</b>
```r
ubuntu@ipv4-public-address:~$ sudo apt-get --purge remove postgresql
```
<b>Remove `pgAdmin4` from your `EC2` compute machine or `Linux` virtual machine</b>
```r
ubuntu@ipv4-public-address:~$ sudo apt autoremove pgadmin4
```
