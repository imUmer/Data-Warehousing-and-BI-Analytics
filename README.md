# Data-Warehousing-and-BI-Analytics

# Hands-on Lab 1: Setting up a staging area

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

# Exercise 3 - Create data warehouse schema
Step 1: Download the schema files.

The commands to create the schema are available in the file below.

[Download file from here](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Setting%20up%20a%20staging%20area/billing-datawarehouse.tgz) 

OR
Run the commands below to download and extract the schema files.

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


# Hands-on Lab 2: Verifying Data Quality for a Data Warehouse
## link of Lab 
 
[Lab Assesment](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse.md.html)
 
## In this lab you will practice how to create and run data quality tests.

Step 1: Start the postgresql server.
```
start_postgres
```

Step 2: Download the staging area setup script.

Run the command below to download the staging area setup script.

```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/setup_staging_area.sh
```
Step 3: Run the setup script.

Run the command below to execute the staging area setup script.

```
bash setup_staging_area.sh
```
When you see a message Successfully setup the staging area you are ready to perform data quality checks.

# Exercise 2 - Getting the testing framework ready
You can perform most of the data quality checks by manually running sql queries on the data warehouse.

It is a good idea to automate these checks using custom programs or tools. Automation helps you to easily

- create new tests,
- run tests,
- and schedule tests.

We will be using a python based framework to run the data quality tests.

Step 1: Download the framework.

Run the commands below to download the framework
```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/dataqualitychecks.py

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/dbconnect.py

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/mytests.py

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/generate-data-quality-report.py


ls
```
Step 2: Install the python driver for Postgresql.

Run the command below to install the python driver for Postgresql database
```
pip install psycopg2
```
Step 3: Test database connectivity.

Now we need to check

- if the Postgresql python driver is installed properly.
- if Postgresql server is up and running.
- if our micro framework can connect to the database.
The command below to check all the above cases.
```
python3 dbconnect.py
```
If all goes well, you should a message Successfully connected to database.

The command also disconnects from the server with a message Connection closed.
# Exercise 3 - Create a sample data quality report
Run the command below to install pandas.
```
pip3 install pandas
```
Run the command below to generate a sample data quality report.
```
python3 generate-data-quality-report.py
```
You should see a list of tests that were run and their status.

# Exercise 4 - Explore the data quality tests
Open the file mytests.py in the editor by using the steps below.

![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/images/file-open.png)

![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/images/select-mytests.py.png)

You should now see the file opened in the editor.

![image](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Verifying%20Data%20Quality%20for%20a%20Data%20Warehouse/images/mytests.py.png)

The file mytests.py contains all the data quality tests.

It provides a quick and easy way to author and run new data quality tests.

The testing framework provides the following tests:

- check_for_nulls - this test will check for nulls in a column
- check_for_min_max - this test will check if the values in a column are - - with a range of min and max values
- check_for_valid_values - this test will check for any invalid values in a column
- check_for_duplicates - this test will check for duplicates in a column

Each test can be authored by mentioning a minimum of 4 parameters.

- testname - The human readable name of the test for reporting purposes
- test - The actual test name that the testing micro framework provides
- table - The table name on which the test is to be performed
- column - The table name on which the test is to be performed

# Exercise 5 - Check for nulls
Let us now see what a check_for_nulls test looks like.

Here is a sample check_for_nulls test:
```
test1={
	"testname":"Check for nulls",
	"test":check_for_nulls,
	"column": "monthid",
	"table": "DimMonth"
}
```
All tests must be named as test following by a unique number to identify the test.

- Give an easy to understand description for testname
- mention check_for_nulls for test
- mention the column name on which you wish to check for nulls
- mention the table name where this column exists

Let us now create a new check_for_nulls test and run it.

The test below checks if there are any null values in the column year in the table DimMonth.

The test fails if nulls exist.

Copy and paste the code below at the end of mytests.py file.
```
test5={
	"testname":"Check for nulls",
	"test":check_for_nulls,
	"column": "year",
	"table": "DimMonth"
}
```
Save the file using Menu -> File -> Save

Run the command below to generate the new data quality report.
```
python3 generate-data-quality-report.py
```
# Exercise 6 - Check for min max range
Let us now see what a check_for_min_max test looks like.

Here is a sample check_for_min_max test
```
test2={
	"testname":"Check for min and max",
	"test":check_for_min_max,
	"column": "monthid",
	"table": "DimMonth",
	"minimum":1,
	"maximum":12
}
```
In addition to the usual fields, you have two more fields here.

- minimum is the lowest valid value for this column. (Example 1 in case of month number)
- maximum is the highest valid value for this column. (Example 12 in case of month number)
Let us now create a new check_for_min_max test and run it.

The test below checks for minimum of 1 and maximum of 4 in the column quarter in the table DimMonth.

The test fails if there any values less than minimum or more than maximum.

Copy and paste the code below at the end of mytests.py file.
```
test6={
        "testname":"Check for min and max",
	"test":check_for_min_max,
	"column": "quarter",
	"table": "DimMonth",
	"minimum":1,
	"maximum":4
}
```
Save the file using Menu -> File -> Save

Run the command below to generate the new data quality report.
```
python3 generate-data-quality-report.py
```
# Exercise 7 - Check for any invalid entries
Let us now see what a check_for_valid_values test looks like.

Here is a sample check_for_valid_values test:
```
test3={
	"testname":"Check for valid values",
	"test":check_for_valid_values,
	"column": "category",
	"table": "DimCustomer",
	"valid_values":{'Individual','Company'}
}
```
In addition to the usual fields, you have an additional field here.

- use the field valid_values to mention what are the valid values for this column.
Let us now create a new check_for_valid_values test and run it.

The test below checks for valid values in the column quartername in the table DimMonth.

The valid values are Q1,Q2,Q3,Q4

The test fails if there any values less than minimum or more than maximum.

Copy and paste the code below at the end of mytests.py file.
```
test7={
	"testname":"Check for valid values",
	"test":check_for_valid_values,
	"column": "quartername",
	"table": "DimMonth",
	"valid_values":{'Q1','Q2','Q3','Q4'}
}
```
Save the file using Menu -> File -> Save

Run the command below to generate the new data quality report.
```
python3 generate-data-quality-report.py
```
# Exercise 8 - Check for duplicate entries
Let us now see what a check_for_duplicates test looks like.

Here is a sample check_for_duplicates test
```
test4={
	"testname":"Check for duplicates",
	"test":check_for_duplicates,
	"column": "monthid",
	"table": "DimMonth"
}
```
Let us now create a new check_for_duplicates test and run it.

The test below checks for any duplicate values in the column customerid in the table DimCustomer.

The test fails if duplicates exist.

Copy and paste the code below at the end of mytests.py file.
```
test8={
	"testname":"Check for duplicates",
	"test":check_for_duplicates,
	"column": "customerid",
	"table": "DimCustomer"
}
```
Save the file using Menu -> File -> Save

Run the command below to generate the new data quality report.
```
python3 generate-data-quality-report.py
```


# Hands-on Lab: Populating a Data Warehouse
[Lab Assesment](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/Populating%20a%20dataware%20house.md.html)

## Exercise 1 - Create an instance of IBM DB2 on cloud
We will be using the cloud instance of IBM DB2 as a production data warehouse in this lab.

If you do not have an instance of IBM DB2 on cloud, follow the instructions in this lab to create one.

## Exercise 2 - Create service credentials
To access your IBM DB2 cloud instance from external programs, you need service credentials.

If you do not have service credentials, follow the instructions in this lab to create your service credentials.

Make a note of the following details:

- user
- password
- host
- port
- database name
You will need them later in this lab.

## Exercise 3 - Create a db2cli dsn
You can access the IBM DB2 cloud instance using the web browser user interface.

Using the `db2cli` you can access your cloud IBM DB2 instance from the command line.

db2cli can be very helpful in automating data load tasks.

In this exercise we will be creating a dsn (data source name). A dsn in short is a simple name that refers to a data source.

Creating a dsn is two step process.

​ Step 1: We add the database, host, port and the security mode details. A sample commmand is given for your reference below:

`db2cli writecfg add -database dbname -host hostname -port 50001 -parameter "SecurityTransportMode=SSL"`

Step 2: We give a name to the data source we just created. This dsn name helps us to easily point to the IBM DB2 instance. A sample commmand is given for your reference below.

`db2cli writecfg add -dsn dsn_name -database dbname -host hostname -port 50001`

Run the commands below on the terminal to create a dsn named `production`. Make sure you use the database name, host and port details you noted in exercise 2.

```
db2cli writecfg add -database BLUDB -host 0c77d6f2-5da9-48a9-81f8-86b520b87518.bs2io90l08kqb1od8lcg.databases.appdomain.cloud -port 31198 -parameter "SecurityTransportMode=SSL"

db2cli writecfg add -dsn production -database BLUDB -host 0c77d6f2-5da9-48a9-81f8-86b520b87518.bs2io90l08kqb1od8lcg.databases.appdomain.cloud -port 31198
```
You should see an output similar to the one below.

![alt figure1](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/images/add-dsn.png)

## Exercise 4 - Verify a db2cli dsn
Now that the dsn is created, we need to verify if it is working, before we go ahead and start using it.

The generic syntax for the command to verify the dsn is given below:

`db2cli validate -dsn alias -connect -user userid -passwd password`

Run the command below to verify the production dsn. Make sure you use your username and password that you noted in Exercise 2.

```
db2cli validate -dsn production -connect -user jrg38634 -passwd SuWySBe5Y4MsYnh9
```

You should see an output similar to the one below.

![alt](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/images/dsn-validation.png)

Your dsn is validated. You can now use it to access the IBM DB2 cloud instance.

## Exercise 5 - Create the schema on production data warehouse
Step 1: Download the schema file.

Run the command below to download the schema file.

```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/star-schema.sql
```
Step 2: Create the schema.

Run the command below to create the schema on the production data warehouse. Make sure you use your username and password that you noted down in Exercise 2.
```
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9 -inputsql star-schema.sql
```
The command above tells db2cli to run the commands in the file star-schema.sql on the production data warehouse.

## Exercise 6 - Populate the production data warehouse
Step 1: Download the data files.

Run the commands below to download the data files.

```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/DimCustomer.sql

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/DimMonth.sql

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/FactBilling.sql

ls *.sql
```

Step 2: Load the data in the data warehouse.

Run the commands below to load the data on to the production data warehouse. Make sure you use your username and password that you noted in Exercise 2.

```
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9 -inputsql DimCustomer.sql
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9 -inputsql DimMonth.sql
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9 -inputsql FactBilling.sql
```

## Exercise 7 - Verify the data on the production data warehouse
Step 1: Download the verification sql file.

Run the command below to download the sql file to verify the data.
```
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/verify.sql
```
Step 2: Verify the data in the data warehouse.

Run the command below to verify the data on the production data warehouse. Make sure you use your username and password that you noted down in Exercise 2.
```
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9 -inputsql verify.sql
```
You have successfully loaded the data, if you see an output similar to the one below.

![alt](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/images/verify.png)

Exercise 8 - Work with db2cli interactive command line
db2cli can also be used interactively.

Run the command below to open an interactive sql command shell to your production data warehouse. Make sure you use your username and password that you noted in Exercise 2.
```
db2cli execsql -dsn production -user jrg38634 -passwd SuWySBe5Y4MsYnh9
```

![alt](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/images/db2-cli-interactive1.png)

Run the command below on the db2cli.
```
select count(*) from DimMonth;
```
You should see an output as seen in the image below.

![alt](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0260EN-SkillsNetwork/labs/Populating%20a%20Data%20Warehouse/images/db2cli-interactive2.png)

You are encouraged to run more sql queries. When done type `quit` to exit db2cli.








