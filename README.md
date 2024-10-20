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

* CHAPTER 4 (CREATE VIEW IN SPARK SQL)
  create or replace view simple_view as select * from emp_csv
  select * from simple_view

* CHAPTER 5 (CREATE TEMP VIEW THIS TEMP VIEW CANT CREATE IN SEPARATE SESSION)

* CHAPTER 6( CREATE GLOBAL VIEW THIS WILL AVAILABLE IN DIFF NOTEBOOK/ WHEN U DEATTACH/ATTACH CLUSTER)
  select * from global_temp.global_view

* CHAPTER 7(NOT NULL)
create table myname(id int, name string not null)
insert into myname values(1,null) ----- gives me error
alter table myname change column drop not null

* CHAPTER 8(CHECK CONSTRAINT)
 create table myname(id int, name string not null)
insert into myname values(1,'VIDHI)
alter table myname add constraint salary1 check (salary>50000)

* CHAPTER 9 (TRUNCATE)
  use truncate when i want to delete whole table
  in csv/delta/parquet format use delete to delete some specific rows

* CHAPTER 10 (DELETE COMMAND WITH SUBQUERY)
  delete from mycity1
  where id in(
  select id
  from city)

* CHAPTER 11 (update command)
    1.  update employee_1
     set city ='patna'
     where (select city from employee_city where city = 'bihar')

    2. update employee_1
       set state = 'lucknw'
       where exists(select city from employee_city where employee_1.city = employee_city.city)

    3. update employee_1
       set salary = 80000
       where id in (select id from employee_city)  
    



  


  



