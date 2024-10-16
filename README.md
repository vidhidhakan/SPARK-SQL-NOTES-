# SPARK-SQL-NOTES-

* CHAPTER 1(CREATE DATABASES) 

Create database mycustomer

Describe database mycustomer

Show databases;

* CHAPTER 2(CREATE TABLES)

create table if not exists mycustomer.pizza_2(customer id int, name string);

describe mycustomer.pizzas_2

describe extended mycustomer.pizzas_2

INSERT INTO mycustomer.pizzas_2 VALUES (1, 'vidhi');

spark.conf.get("spark.sql.warehouse.dir") ------- to check my directory 

%fs ls dbfs:/user/hive/warehouse/mycustomer.db/pizzas_1 ------------ to check my path 

* CHAPTER 3 (INTERNAL/MANAGED TABLE)

  (THIS WILL DELETE MY INSIDE DATA AND OUTSIDE BCZ I DIDNT GIVE THEM A LOCATION SO BY DEFAULT
  WHEN MY CLUSTER TERMINATE MY TABLE WILL GONNA DELETE)

* CHAPTER 4 (EXTERNAL TABLE) 

  (THIS WILL DELETE ONLY MY METADATA BUT MY ACTUAL DATA WILL BE STORE AS I PROVIDE MY LOCATION
  SO IT WONT DELETE EVEN IF MY CLUSTER TERMINATES)
  
create table mycustomer.external_table1(id int, name string) 
using delta 
location "/spark_sql/external_tables/external_table1" 
tblproperties ( 
  'Type' = 'External', 
  'delta.minReaderVersion' ='1', 
  'delta.minWriterVersion' = '2' 
)  

* CHAPTER 4 (CREATE TABLE USING CSV FILE)

FROM PYSPARK.SQL.TYPES IMPORT *

  



