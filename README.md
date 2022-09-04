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


# Hands-on Lab 2: Verifying Data Quality for a Data Warehouse

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


















