Learn how to create a database and a table now that you've successfully completed Parts 1 and 2.<br>

1. Connect to your EC2 compute machine : open terminal and SSH to your EC2 instance<br>

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-24.png](https://i.postimg.cc/Rqx6yvtr/isaac-arnault-aws-24.png)](https://postimg.cc/QKSdWGSS)

</p>
</details>

2. Create new database<br>

```r
$ sudo su -l postgres
$ psql
postgres=# CREATE DATABASE github; # creates a database called github
postgres=# \l # lists all databases on your PostgreSQL server - you have a postgres database by default
```

<details>
<summary>🔴 See output</summary>
<p>  
  
[![isaac-arnault-aws-26.png](https://i.postimg.cc/vHwJ8D5J/isaac-arnault-aws-26.png)](https://postimg.cc/5jp7n47g)
  
</p>
</details>


3. Go to pgAdmin4 and refresh your server : right click to refresh<br>
You should now be able to see your newly database <b>github</b>created.<br>
Click on the <b>Dashboard</b> tab to see live charts related to your PostreSQL database server such as:<br>
  > <b>Transactions per second</b><br>
  <b>Tuples in</b><br>
  <b>Tuples out</b><br>
  <b>Block I/O</b><br>
  <b>PID</b><br>

<details>
<summary>🔴 See output</summary>
<p>
  
[![isaac-arnault-aws-28.png](https://i.postimg.cc/WbKJJL1c/isaac-arnault-aws-28.png)](https://postimg.cc/7f3LpRzK)
  
</p>
</details>
  
Right click on database <b>github</b> > properties, fill the comment section and click on <b>Save</b>.

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-aws-28.png](https://i.postimg.cc/T3M36RP1/isaac-arnault-aws-28.png)](https://postimg.cc/vchs7wfw)
  
</p>
</details>

4. If we click on <b>SQL</b> tab, we'll have the SQL syntax of your database called "github".

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-aws-30.png](https://i.postimg.cc/0j7263WP/isaac-arnault-aws-30.png)](https://postimg.cc/0K2qFt1B)
  
</p>
</details>

5. Let's go back to our EC2 instance compute machine to perform some Postgres commands.<br>
We'll now create our fist table in our <b>github</b> database.

```r
postgres=# \c github # to allow user postgres to connect to the database "github"
postgres=# CREATE TABLE clients (
ID serial primary key,
NAME text,
SURNAME text,
GENDER text,
AGE integer,
COUNTRY text,
PURCHASE integer,
VENUE date
);
postgres=# SELECT * FROM clients;
```
<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-aws-31.png](https://i.postimg.cc/3JZqZTcV/isaac-arnault-aws-31.png)](https://postimg.cc/JGGK19m5)
  
</p>
</details>

Now we are going to insert multiple data into our <b>clients</b> table in just one SQL query :

```r
INSERT INTO clients (ID, NAME, SURNAME, GENDER, AGE, COUNTRY, PURCHASE, VENUE) VALUES
    (1, 'Luiz', 'Marciano', 'Male', 45, 'Brazil', 1450.00, '1999-01-08'),
    (2, 'Maria', 'Kukushka', 'Female', 21, 'Belarus', 230.00, '2014-11-21'),
    (3, 'Manuel', 'Ortega', 'Male', 32, 'Spain', 1350.00, '2003-07-14'),
    (4, 'Gwendal', 'Dupond', 'Male', 32, 'France', 2825.00, '2010-02-17');    
```
For date/time types, feel free to check : https://www.postgresql.org/docs/9.1/datatype-datetime.html<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-aws-32.png](https://i.postimg.cc/43vHYWd6/isaac-arnault-aws-32.png)](https://postimg.cc/yJd85X0x)

</p>
</details>

Now let's go back to `pgadmin4` and refresh our `PostgreSQL` server.<br>

Go to databases > github > schema > tables we can see our <b>clients</b> table.<br>
Right click on the table > View/Edit data > First 100 Rows<br>
As we can see, our table <b>clients</b> is shown along with all data inserted using our `EC2` compute machine.<br>

<details>
<summary>🔴 See output</summary>
<p>

[![isaac-arnault-aws-33.png](https://i.postimg.cc/BQ168m7j/isaac-arnault-aws-33.png)](https://postimg.cc/SJkq3fh4)

</p>
</details>

If we click on the <b>Statistics</b> tab, we'll see some useful stats related to the table we've just created.

<details>
<summary>🔴 See output</summary>
<p>

[![isaac-arnault-AWS-34.png](https://i.postimg.cc/XYSv99tQ/isaac-arnault-AWS-34.png)](https://postimg.cc/w72HpRqm)

</p>
</details>

If you are not technical and you would like to bypass the `Command Line Interface`, you can perform the same <b>table creation</b> task using `pgAdmin4` available tools above the application.<br>

[![isaac-arnault-aws-34.png](https://i.postimg.cc/NM30bT5s/isaac-arnault-aws-34.png)](https://postimg.cc/ygTB8Dmt)


Now we have an `EC2` compute machine and a `PostgreSQL` database running, as well as one table created... all fully operational and ready for production. Feel free to check the <b>HINTS</b> section of this gist to get other useful commands related to `PostgreSQL`.<br>
Please fork this gist if you find it useful and for showing support. Many thanks.
