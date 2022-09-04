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

- -h mentions that the database server is running on the localhost
- -U mentions that we are using the user name postgres to log into the database
- -p mentions that the database server is running on port number 5432
You should see an output like this.

![alt ide](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/images/postgres-createdb.png)

#Exercise 3 - Create data warehouse schema
Step 1: Download the schema files.

The commands to create the schema are available in the file below.
(https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/billing-datawarehouse.tgz) Run the commands below to download and extract the schema files.
```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/billing-datawarehouse.tgz

tar -xvzf billing-datawarehouse.tgz
ls *.sql
```
You should see 4 .sql files listed in the output

Step 2: Create the schema

Run the command below to create the schema in the billingDW database.
```
psql  -h localhost -U postgres -p 5432 billingDW < star-schema.sql
```
You should see an output similar to the one below.
![alt IDE]![image](https://user-images.githubusercontent.com/57424391/188310412-56181628-478d-4503-bd0a-d87a46ef4726.png)

# Exercise 4 - Load data into Dimension tables
When we load data into the tables, it is a good practice to load the data into dimension tables first.

Step 1: Load data into DimCustomer table

Run the command below to load the data into DimCustomer table in billingDW database.
```
psql  -h localhost -U postgres -p 5432 billingDW < DimCustomer.sql
```
Step 2: Load data into DimMonth table

Run the command below to load the data into DimMonth table in billingDW database.
```
psql  -h localhost -U postgres -p 5432 billingDW < DimMonth.sql
```
# Exercise 5 - Load data into Fact table
Load data into FactBilling table

Run the command below to load the data into FactBilling table in billingDW database.
```
psql  -h localhost -U postgres -p 5432 billingDW < FactBilling.sql
```
# Exercise 6 - Run a sample query
Run the command below to check the number of rows in all the tables in the billingDW database.
```
psql  -h localhost -U postgres -p 5432 billingDW < verify.sql
```
You should see an output similar to the one below.

![alt IDE](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/images/verify.png)

Your data warehouse staging area is now ready.
