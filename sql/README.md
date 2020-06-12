## SQL Notes

Chapter 1:
1. Each table has a unique name and its columns are fields.
2. Multiple fields can be selected with
  ``` SELECT a,b,c FROM tablename```
3. Distinct or unique elements of columns(particular or many) can be selected with 

        SELECT DISTINCT country FROM people
      
4. Number of elements in a table or field can be calculated with COUNT()

        SELECT COUNT(country) FROM people
        SELECT COUNT(DISTINCT country) FROM people

Chapter 2: Conditioning with WHERE, AND and OR

1. WHERE, AND can be used for quering condition to get the desired result
        
        SELECT * FROM films WHERE rating='r' AND release_year>2000       
        
2. when AND and OR are used multiple times in query. seperating which one belongs to which is crucial. Seperation can be done with ( )
        
         SELECT title,release_year FROM films where (language='Spanish' or language='French') and 
         (release_year<2000 and release_year>=1990) and gross>2000000
         
 3. To avoid redundancy by repeating column name twice or thrice There is BETWEEN keyword to filter numbers within specified range. The range is inclusive i.e 1990 and both 2000 are included in the filtered table
 
           SELECT title,release_year FROM films where (language='Spanish' or language='French') and 
           (release_year BETWEEN 1990 AND 2000 ) and gross>2000000
 
 4. Chaining OR multiple times can be time consuming and unwieldy. For sane reasons there is IN keyword
          
          SELECT name
          FROM kids
          WHERE age = 2
          OR age = 4
          OR age = 6
          OR age = 8
          OR age = 10;
          
          SELECT name FROM kids where age IN (2,4,6,8,10);
          
5. IS NULL checks for NULL values i.e values that are not filled within field
to check people who have not died yet.

        SELECT * from people WHERE deathdate is NULL

Chapter 3: Wildcards in SQL

1. % character will match 0 or more characters in the text. Comparing with regex its ``` .* ``` . It has to be used with LIKE keyword.``` Data% ``` will match Datacamp Data DataC 

         SELECT * FROM coursesellers WHERE name like 'Data%'
2. _ will match one character. ``` ash_ish ``` will match ashish ashash 
  
         SELECT * FROM people where name like  'ash_sh'    
   
3. To invert matched pattern use NOT LIKE     
    
          SELECT * FROM PEOPLE where name NOT LIKE 'Samiks%'

Chapter 4: Aggregate functions

Average, Mean, Median, Standard Deviation , Mode, maximum, minimum, sum etc are aggregate functions 

          SELECT (MAX(release_year)-MIN(release_year)/10) as decades from films 


Chapter 5: ORDERING
```ORDER BY```
1. For ordering in ascending order
  
         select * from people where name like 'K%' order by name
  
  add DESC at the end to sort in descending order
         
         select * from people where name like 'K%' order by name DESC

``` GROUP BY```

1. Used with aggregate functions, This will group the row elements according to selected field

        select country,max(income) from people group by country order by country
 
 This will return richest person from each country from database
 
 
 Chapter 6: HAVING
 
 Suppose i want to get the name of the film which has maximum view time. How would i do that?
My solution is to first find the highest viewcount then select from table where viewcount is highest viewcount

        SELECT MAX(view_count) from films   --Output
        SELECT name from films where view_count=Output
        
Another way is by using ```HAVING```
        
        SELECT name from films HAVING view_count=MAX(view_count)
        
## Inner join in SQL

1. two tables whose key matches are joined. Others are discarded.

         
              select c.code as country_code,c.name,e.year,e.inflation_rate
              FROM countries AS c
              INNER JOIN economies as e
              ON c.code=e.code
              
2. Instead of using ON clause, one can use USING clause
        
          select c.code as country_code,c.name,e.year,e.inflation_rate
              FROM countries AS c
              INNER JOIN economies as e
              USING (code)
              
## Self join 

They are used to compare values in the field with another value in the same field from within the same table. 


       
      

