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
    
 
* CHAPTER 12 (RESTORE)- VERSION IS ONLY AVIALBLE IN DELTA TABLE
   restore table employee_1  version as of 1
   restore table employee_1  timestamp as of

* CHAPTER 13(MERGE)
  MERGE INTO merge1 AS m1
  
  USING merge2 AS m2
  
  ON m1.id = m2.id
  
  WHEN MATCHED THEN
  
   UPDATE SET
  
    m1.name = m2.name,
  
    m1.gender = m2.gender,
  
    m1.salary = m2.salary,
  
    m1.city = m2.city,
  
    m1.state = m2.state
  
WHEN NOT MATCHED THEN

  INSERT (id, name, salary, gender, city, state)
  
  VALUES (m2.id, m2.name, m2.salary, m2.gender, m2.city, m2.state);

 * CHAPTER 14(MERGE WITH DELETE COMMAND)
   
    MERGE INTO vidhi AS v
    
    USING piyush AS p
    
    ON v.id = p.id

   WHEN MATCHED AND p.city = 'rajkot' THEN
   
    DELETE

  WHEN NOT MATCHED THEN
  
    INSERT (id, name, gender, city)
    
    VALUES (p.id, p.name, p.gender, p.city);

  * CHAPTER 15(INTERSECT) -- when i want to see common things
    select * from vidhi1 intersect select * from vidhi2;

  * CHAPTER 16(EXCEPT/EXCEPT ALL) --- except - (first table contain unique values )remove dulicates/ except all(include 
 duplicates from 1st table

  * CHAPTER 17(WINDOW FUNCTION)-- USED WHEN I NEED TO DO ORDERING/PARTITIONG BASED ON SPECIFIC ROWS NOT DATSET
    rank() will skip rows eg -- 1,1,starts with 3
    
    denserank() wont skip rows eg --1,1,2,3,3,4
    
    rownumber() givenumber -- 1,2,3,4,
    
    sum(salary)over (partition by state order by salary desc), avg,max,min,count -- sameway

* CHAPTER(18) LEAD
  
lead - if i want to see next row
lag - if i want to see previous row

lead(salesamount,2) over (partitioned by year order by id asc) as totalsales
lag(salesamount,1) over (partitioned by year order by ids desc) as totalsales

* CHAPTER (19) COLLECT LIST/SET
  Select collect_list(salary) from yas1
  select collect_set(salary) from yas1
     
* CHAPTER (20)- CONCAT
  select('employee',' ',name,' ',salary)from yas1

* CHAPTER(21) concat_ws() --- this will include separator evernthough if its null it wont give extra space
  select concat_ws(" ",name,salesamount) as totalsalary from yas1

* CHAPTER(22) contains--- this use to see whether my value is true/false
  select name,contains(name,'vidhi') from yas1

* CHAPTER(23)date_add(): Adds or subtracts a specific number of days from a date
  
  syntax : dateadd(start_date,num_days) -- select * , date_add(sales_date,10) from pizza

* CHAPTER 24 -  datediff(): Finds the difference between two dates in terms of days.
   select *, date_diff(sales_date,order_date) from pizza1
  

  
  
  
  
  

   
  
  


  


  



