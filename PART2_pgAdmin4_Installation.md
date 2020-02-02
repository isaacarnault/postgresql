### Part 2. Deploy pgadmin4 on your EC2 instance to administrate your database (front-end)<br>

After completing Part 1, you are now ready to install `pgAdmin4` which will help you administrate your database and see jobs performed on your `EC2` compute machine.<br>

1. Log into your `EC2` instance in SSH (see Part 1 , 7) and perform as follows :

```r
sudo apt update
sudo apt install pgadmin4 pgadmin4-apache2 -y
```
When prompted by your `Terminal`, leave settings as default and <b>OK</b>.<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-15.png](https://i.postimg.cc/tTjyQ8cQ/isaac-arnault-aws-15.png)](https://postimg.cc/XZQt913Q)

</p>
</details>

2. Set initial `pgAdmin4` password and <b>OK</b>.<br>

<details>
<summary>🔴 See hint</summary>
<p>  
  
[![isaac-arnault-aws-16.png](https://i.postimg.cc/L54phLRx/isaac-arnault-aws-16.png)](https://postimg.cc/7GRcWC5z)

</p>
</details>

3. Check if Apache service is started on your `EC2` compute machine.

```r
$ systemctl status apache2
```

4. Allow http and https traffic from your `EC2` compute machine to the `Internet`.<br>
See HINTS section part of this gist if you have problems displaying `pgAdmin4` viewer on your browser.

```r
sudo ufw allow http
sudo ufw allow https
```

<details>
<summary>🔴 See hint</summary>
<p>  
  
[![isaac-arnault-aws-17.png](https://i.postimg.cc/d33xzBJc/isaac-arnault-aws-17.png)](https://postimg.cc/2LpGWnq0)

</p>
</details>

5. Open your web browser and enter your `IPv4` public address (you can find it on AWS on your EC2 console) and the listening port of `pgAdmin4` which is 5432.<br>
  | i.e: my-ipv4-address/pgadmin4/browser<br>
  | use following login details to log into pgAdmin4<br>
  <b>ID</b>: postgres@localhost <b>Pwd</b>: the one you've chosen upon PostgreSQL server configuration<br>
  
<details>
<summary>🔵 See application</summary>
<p>
  
[![isaac-arnault-aws-21.png](https://i.postimg.cc/QN98KGLD/isaac-arnault-aws-21.png)](https://postimg.cc/s1zdbLDH)  
  
</p>
</details>

6. Once logged in, click on Servers > Add New Server<br>

<details>
<summary>🔵 See application</summary>
<p>
  
[![isaac-arnault-aws-22.png](https://i.postimg.cc/L5zGkVBt/isaac-arnault-aws-22.png)](https://postimg.cc/XBY24dPq)

</p>
</details>

For server configuration set the following fields as follows:<br>
  > <b>Name</b> : postgres<br>
  <b>Hostname/address</b> : localhost<br>
  <b>Username</b> : postgres<br>
  <b>Password</b> : the one you've chosen upon server configuration<br>

<details>
<summary>🔵 See setting</summary>
<p>
  
[![isaac-arnault-aws-23.png](https://i.postimg.cc/63x0VxHP/isaac-arnault-aws-23.png)](https://postimg.cc/GBzGrVnP)

</p>
</details>

Then click on <b>Save</b>.<br>
There you are !<br>

<details>
<summary>🔵 See application</summary>
<p>
  
  
</p>
</details>

Your `PostgreSQL` server is setted correctly on your `EC2` instance and accessible via `pgAdmin4`.<br>
You can now take part 3 of this gist. You'll learn how to create a database, a table on your `EC2` compute machine and perform some administration tasks via `pgAdmin4`.
