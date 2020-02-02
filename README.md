[![isaac-arnault.png](https://i.postimg.cc/C5pKYvzq/isaac-arnault.png)](https://postimg.cc/Q9SDJJg8)

# PostgreSQL integration & setting up: one effective way
    • Database: PostgreSQL
    • Programming : Shell (bash), SQL
    • Cloud: AWS
    • OS : Linux
    • Distribution : this gist works on Ubuntu 19.10 eoan (on prem'), Ubuntu 18.04 LTS (AWS)
  
### Gist writing, testing and debugging : 12 hrs - Author :  Isaac Arnault - License : MIT©, 2020

[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)

The following gist is intended to Data Architects and is part of my `AWS` cloud series.<br>
It will help you start with `PostgreSQL` on `AWS`.<br>
Since `Postgres` is the one of the most advanced `SQL` or relational databases, you may want to consider it for a professional use.<br>
Please fork it if you find this useful.

## How is gist is structured
This gist is structured into 3 parts.<br>
You are invited to take each part one after the other.<br>

<b>Part 1. Deploy PostgresSQL 12 on a Linux system using AWS EC2 (back-end)</b><br>
<b>Part 2. Deploy pgadmin4 on your EC2 instance to administrate your database (front)</b><br>
<b>Part 3. Start with PostgreSQL 12 on back-end (EC2) and check your tasks on pgAdmin4 (front-end)</b>

# Few words before we start
`PostgreSQL` is a free and open-source powerful relational database management system (`RDBMS`) designed to handle many workloads, from single VMs to datawarehouses. <br> If you are a `Data Engineer` or `Data Architect` you may be familiar with `ACID` properties of relational databases. <br> Please note that `PostgreSQL` guarantees Atomicity, Consistency, Isolation and Durability of your databases.

  | <b>Some useful resources</b><br>
. Encyclopedical : https://en.wikipedia.org/wiki/PostgreSQL - English<br>
. Practical : https://waytolearnx.com/2018/11/difference-entre-mysql-et-postgresql.html - French<br>
. Tactical : https://fr.slideshare.net/EnterpriseDB/postgresql-12-what-is-coming-up-enterprise-postgres-day - English<br>

## Related tags

    • AWS
    • EC2
    • PostgreSQL
    • Postgres
    • pgAdmin4
    • SQL
    • RDBMS
    • Cloud computing
<hr>
About the author : Isaac Arnault is Big Data Architect, https://isaacarnault.github.io.
