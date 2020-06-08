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
 
 
