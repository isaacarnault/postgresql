### Part 1. Deploy PostgresSQL 12 on a Linux system using AWS EC2 (back)

1. Log into your `AWS` console, https://signin.aws.amazon.com/.<br>
In order to enhance the security access of my root account, I have `MFA` activated on my `AWS` account. I advise you to do so.<br>

<details>
<summary>🔴 See hint</summary>
<p>
  
Once logged into your account, click on `EC2`.

[![isaacarnault-aws.png](https://i.postimg.cc/wvgmQTQP/isaacarnault-aws.png)](https://postimg.cc/f3qywsFj)

</p>
</details>

  > !! Please note that `AWS` has a new layout interface which is pretty cool !!

2. Click on Instances > Launch instance

<details>
<summary>🔴 See hint</summary>
<p>
  
[![isaac-arnault-aws2.png](https://i.postimg.cc/BvZqW2kZ/isaac-arnault-aws2.png)](https://postimg.cc/VJTyn0z2)

</p>
</details>

3. Select Ubuntu Server 18.04 LTS (HVM)

<details>
<summary>🔴 See hint</summary>
<p>

[![isaac-arnault-aws-3.png](https://i.postimg.cc/HkBqyRvH/isaac-arnault-aws-3.png)](https://postimg.cc/yD3pqQzr)
  
</p>
</details>

  | <b>Hint</b> : You can perform installation of `PostgreSQL 12` and `pgAdmin4` on a `Ubuntu 19.10 eoan` distribution, which is not currently available on `AWS`.
  
4. Choose a free tier eligible instance for the purposes of your test. <br>

You may consider more robust instances plans if you want your database to support concurrent workloads.

<details>
<summary>🔴 See hint</summary>
<p>
  
[![instance.png](https://i.postimg.cc/28s2jmCt/instance.png)](https://postimg.cc/w7khFCy5)

</p>
</details>

  > Review and Launch > Launch<br>
  Create a new key pair > Key pair name : <b>PostgresKP</b> > Download key pair<br>
  Click on Launch instances > View instances

<details>
<summary>🔴 See hint</summary>
<p>

[![isaac-arnault-aws-5.png](https://i.postimg.cc/2jghz5zN/isaac-arnault-aws-5.png)](https://postimg.cc/YjfhRMGd)
  
</p>
</details>

5. Once your instance is deployed (2/2 checks), go to Actions > Instance settings > Change termination protection<br>
Click on "Yes, enable". This will prevent your `EC2` instance to terminate accidentally.<br>

<details>
<summary>🔴 See hint</summary>
<p>

[![isaac-arnault-aws-19.png](https://i.postimg.cc/YqGdwjBg/isaac-arnault-aws-19.png)](https://postimg.cc/Cz0GGh1L)

</p>
</details>

Now you are ready to go for some `Shell` commands.<br>

6. Connect to your `EC2` instance using Open SSH on your Terminal<br>
<hr>
If you don't have `Open SSH` installed on your `Terminal`, use as follows:

```r
sudo apt update
sudo apt install openssh-server
```
<hr>

We have to remember that we've downloaded an Postgres.pem file earlier. We will now move this file to a newly created directory.<br>

```r
Ctrl + Alt + T # to open a new CLI window<br>
$ cd Desktop > $ mkdir SSH` # Creates an SSH directory to store our Key Pair (credentials)
$ cd Downloads` > `$ sudo mv /home/zaki/Downloads/Postgres.pem /home/zaki/Desktop>SSH`
```
Go to your SSH directory and check that the file persists there :

```r
$ cd Desktop/SSH` > ls
```

- We change the permissions to .pem file, ie:

```r
$ chmod 400 PostgresKP.pem`
```

<details>
<summary>🔴 See hint</summary>
<p>  
  
[![isaac-arnault-aws-6.png](https://i.postimg.cc/MGhfzPSb/isaac-arnault-aws-6.png)](https://postimg.cc/HJ9k2tjV)

</p>
</details>

7. We can now connect to our EC2 instance<br>

```r
$ ssh -i "PostgresKP.pem" ubuntu@ec2-your-ipv4-public-address.compute-1.amazonaws.com
```

- Type "yes" when prompted by the `CLI`<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-8.png](https://i.postimg.cc/HL2594DQ/isaac-arnault-aws-8.png)](https://postimg.cc/mcPtb9rD)

</p>
</details>

<hr>
<b>Important</b>
If you can't connect to your EC2 instance from SSH, feel free to retake another gist I posted months ago where I give you few other hints : <br>
  | * [Deploying a Wordpress site using AWS RDS and free tier EC2 instance - Hands-on](https://gist.github.com/isaacarnault/8c701f200699176e06362a1877909665)
<hr>

8. Check that everything is setting up correctly and start installing Postgres

```r
$ lsb_release -a # this retrives information regarding your EC2 instance (your virtual compute machine)
```
<hr>

Now you are ready to deep dive into PostgreSQL installation on AWS.

#### 1. Install PostgreSQL server on your EC2 instance

To install `PostgreSQL 12` perform as follows:

```r
$ sudo su
$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - # this will import GPG key and add PostgreSQL 12 repository into our Ubuntu EC2 machine
$ echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list # this will add add repository contents into our Ubuntu Ubuntu EC2 machine
$ sudo apt update
$ sudo apt -y install postgresql-12 postgresql-client-12 # this will install the latest available version
```
Once installation is complete, you can check your PostgreSQL server status.<br>

#### 2. Check PostgreSQL service status
```r
$ cd
$ cd /etc/init.d
$ ./postgresql status
```
If `PostgreSQL 12` was correctly installed and is active, you should have this :<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-9.png](https://i.postimg.cc/02DL2b1T/isaac-arnault-aws-9.png)](https://postimg.cc/Yh2Xd29R)

</p>
</details>

If not, feel free to restart the server.<br>

```r
$ ./postgresql restart
$ ./postgresql status
```

We can also check all packages installed related to our `PostgreSQL` server by doing a `grep` command.

```r
$ dpkg -l | grep postgres
```
<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-10.png](https://i.postimg.cc/RC77SH05/isaac-arnault-aws-10.png)](https://postimg.cc/YjSG8jgb)

</p>
</details>


#### 3. Configure PostgreSQL server

```r
$ sudo nano /etc/postgresql/12/main/postgresql.conf
```
Search for listen_addresses and replace as follows :

```r
listen_addresses = '*'
```
<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws10.png](https://i.postimg.cc/pLC94fkk/isaac-arnault-aws10.png)](https://postimg.cc/ZW9KyyGy)
Ctrl + S to save the conf file, Ctrl + X to exit.<br>

</p>
</details>

#### 4. Restart PostgreSQL service

```r
$ sudo systemctl restart postgresql
```
After restarting `PostgreSQL` server, confirm the server is listening on port 5432 using a `netstat` command:<br>

```r
$ sudo netstat -antup | grep 5432
```

<details>
<summary>🔴 See output</summary>
<p>

[![isaac-arnault-aws11.png](https://i.postimg.cc/B6cRBvJ8/isaac-arnault-aws11.png)](https://postimg.cc/8Jcy1NJD)

</p>
</details>

#### 5. Access PotgreSQL

```r
$ sudo su -l postgres
$ psql
```

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-aws-12.png](https://i.postimg.cc/QtVCwVdz/isaac-arnault-aws-12.png)](https://postimg.cc/tZQ9VqPd)

</p>
</details>

#### 6. Secure PostgreSQL database
This step is very important because you might encounter restrictions if your database server is not properly set regarding users access.

6.1 Set password for Linux user (postgres)
```r
$ sudo su
$ passwd postgres
```

<details>
<summary>🔴 See hint</summary>
<p>
  
[![isaac-arnault-aws-13.png](https://i.postimg.cc/q72C4V1p/isaac-arnault-aws-13.png)](https://postimg.cc/Y4qSzVcP)

</p>
</details>

6.2 Set password for DB administrator (postgres)
```r
su - postgres
psql
```
<details>
<summary>🔴 See hint</summary>
<p>
  
[![isaac-arnault-aws-14.png](https://i.postimg.cc/3NxyXyYw/isaac-arnault-aws-14.png)](https://postimg.cc/jwBdKSWV)

</p>
</details>

6.3 Test PostgreSQL connection

<details>
<summary>🔴 See hint</summary>
<p>
 
[![isaac-arnault-aws-18.png](https://i.postimg.cc/rsztxdN9/isaac-arnault-aws-18.png)](https://postimg.cc/fSnLhRF3)

</p>
</details>

Now that you've installed `PostgreSQL` server on your `EC2L` instance and set both passwords for <b>Linux user</b> and <b>DB administrator</b>, you are ready to take part 2 of this gist.
