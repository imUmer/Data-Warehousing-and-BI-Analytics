# Data-Warehousing-and-BI-Analytics

# Hands-on Lab: Setting up a staging area

# Exercise 1 - Start the PostgreSQL server

We will be using the PostgreSQL server as our staging server.

Start the PostgreSQL server.

Open a new terminal, by clicking on the menu bar and selecting Terminal->New Terminal, as shown in the image below.

![alt ide](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/images/new-terminal.png)

This will open a new terminal at the bottom of the screen.

![alt ide](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/images/terminal_bottom_screen.png)

Run the commands below on the newly opened terminal. (You can copy the code by clicking on the little copy button on the bottom right of the codeblock below and then paste it, wherever you wish.)

Start the PostgreSQL server, by running the command below:
```
start_postgres
```
You should see an output similar to the one below.

![alt ide](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/images/start-postgres.png)

# Exercise 2 - Create Database
Create the database on the data warehouse.

Using the createdb command of the PostgreSQL server, we can directly create the database from the terminal.

Run the command below to create a database named billingDW.
```
createdb -h localhost -U postgres -p 5432 billingDW
```
In the above command

-h mentions that the database server is running on the localhost
-U mentions that we are using the user name postgres to log into the database
-p mentions that the database server is running on port number 5432
You should see an output like this.

