# SPARK-SQL-NOTES-

* CHAPTER 1(CREATE DATABASE/ CREATE TABLES/)
databases

Create database mycustomer

Describe database mycustomer

Show databases;

* CHAPTER 2(CREATE TABLES)

create table if not exists mycustomer.pizza_2(customer id int, name string);

describe mycustomer.pizzas_2

describe extended mycustomer.pizzas_2

INSERT INTO mycustomer.pizzas_2 VALUES (1, 'vidhi');

spark.conf.get("spark.sql.warehouse.dir") ------- to check my directory 

%fs ls dbfs:/user/hive/warehouse/mycustomer.db/pizzas_1







