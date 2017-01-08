# SQL notes
> [reference website](www.runoob.com/sql)

## SQL bastic syntax
1. select
   - <code>select colum_name,colum_name from table_name</code>
   - <code>select * from table_name</code>
2. select distinct
  - <code>select distinct column_name,comumn_name form table_name</code>  Duplicate, only select once
3. where
  - <code>select column_name,column_name from table_name where column_name operator value  </code>
  - condition:
  <code>=</code>,
  <code><></code>not equal,
  <code>></code>,
  <code><</code>,
  <code>>=</code>,
  <code>between</code> in a certain range,
  <code>like</code>,
  <code>in</code> Specifies possible values for a column.
4. and & or
  - <code>select * from tabe where column1 > 12 and (field="one" or field="two")</code>
5. order by
  - <code>asc</code>and<code>desc</code>
  - <code>select * from Websites
order by alexa desc;</code>
6. insert into
  - <code>insert into table_name</code><code>values</code> <code>(value1, value2, ... )</code>
  - <code>insert into table_name (column1, column2, ... ) values (value1, value2, ... )</code>
7. update
  - <code>update</code> table_name <code>set</code> column1=value1, column2=value2, ... where some_comumn=some_value;
8. delete
  - <code>delete from</code> table_name where some_column= some_value;

## SQL advanced syntax

1. select top, limit, rownum
  - <code>select top</code><code>20 percent * from test</code> SQL Server /MS Access syntax
  - <code>select</code><code>* from persons</code><code>limit </code> <code>5</code>
2. Wildcards
  - <code>%</code>,<code>\_</code>,<code>[charlist]</code>,<code>[^charlist]</code>and<code>[!charlist]</code>
3. in
4. between
  - value is <code>number</code>,<code>string</code>,<code>date</code>
5. as
6. JOIN
  - <code>inner join</code>. SELECT Websites.id, Websites.name, access_log.count, access_log.date FROM Websites <code>INNER JOIN</code> access_log <code>ON</code> Websites.id=access_log.site_id;
  - <code>left join</code>
  - <code>right join</code>
  - <code>full join</code>
7. union
  - <code>union</code> merge the result set of two or more SELECT statements. important, select a different value.
  - <code>union all</code> contain the same value.
8. SELECT INTO  
  - <code>select * into newtalbe from table1</code>
  - <code>select column_name(s) into newtable from table1</code>
9. INSERT INTO SELECT
  - <code>insert into table2 select * from table1</code>
  - <code>insert into table2 (column_name(s)) select column_name(s) from table1</code>
10. CREATE DATABASE
