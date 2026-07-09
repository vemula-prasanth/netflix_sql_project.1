# netflix movies and tv shows data analysis using sql

![netflix logo](https://github.com/vemula-prasanth/netflix_sql_project.1/blob/main/netflix%20logo.jpeg)

## overview

​This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

## objective

​Analyze the distribution of content types (movies vs TV shows).
​Identify the most common ratings for movies and TV shows.
​List and analyze content based on release years, countries, and durations.
​Explore and categorize content based on specific criteria and keywords.

## dataset

​The data for this project is sourced from the Kaggle dataset:
​Dataset Link:https://www.kaggle.com/datasets/shivamb/netflix-shows

## schema
```sql
drop table if exists netflix;
```
```sql

CREATE TABLE netflix
(
    show_id VARCHAR(6),
    type VARCHAR(10),
    title VARCHAR(150),
    director VARCHAR(208),
    casts VARCHAR(1000),
    country VARCHAR(150),
    date_added VARCHAR(50),
    release_year INT,
    rating VARCHAR(10),
    duration VARCHAR(15),
    listed_in VARCHAR(100),
    description VARCHAR(250)
);
```


## 25 business problems and solutions 

### 1. Count the number of Movies vs TV Shows
```sql
select* from netflix;

select 
      type,
	  count(*) as total_content
from netflix
group by type;
```

### 2. Find the most common rating for movies and TV shows
```sql
SELECT
     type,
	 rating,
	 COUNT(*) as total
FROM netflix
GROUP BY type, rating 
ORDER BY COUNT(*) DESC;
```

### 3. List all movies released in a specific year (e.g., 2020)
```sql
select * from netflix
where 
     type = 'Movie'
	 and 
	 release_year = 2020;
```
 


### 4. Find the top 5 countries with the most content on Netflix
```sql
SELECT Country,
         count(*) as total_content
from netflix
group by Country
order by total_content desc 
limit 5;
```

### 5. Identify the longest movie ?
```sql
select * from netflix
       where
	   type = 'Movie' 
	   and  
	  duration =( select max (duration) from netflix );
	         
```
 
### 6. Find content added in 2021
```sql
select * from netflix 
       where date_added >='2021-01-01';

```

### 7. Find all the movies/TV shows by director 'Rajiv Chilaka'!
```sql
select * from netflix
      where 
	  director ilike '%Rajiv Chilaka%';
   ```
	
 
### 8. List all TV shows with more than 5 seasons
 ```sql
select * from  netflix
       where type = 'TV Show'
	   and 
	   duration > '5 seasons';
       
```

 
### 9. Count the number of content items in each genre
```sql
    select listed_in, 
	       count(*) as total_content from netflix
		   group by listed_in
		   order by total_content desc ;
```
 
### 10. Find the average release year for content produced in a specific country
```sql
        select country,
		       avg(release_year) as avg_year
			   from netflix
			   group by country;

```
 
### 11. List all movies that are documentaries
```sql
select * from netflix
     where listed_in ilike '%Documentaries%';

```
 
### 12. Find all content without a director
 ```sql
select * from netflix
    where director is NULL;

```
 
### 13. Find how many movies actor 'Salman Khan' appeared in last 10 years!
 ```sql
      select * from netflix
             where Casts like '%Salman Khan%' 
			 and 
			 release_year > extract(year from current_date)-10;
 ```
### 14. Find the top 10 actors who have appeared in the highest number of movies produced in
```sql
      select casts, count(*) as total_movies
	         from netflix
			 group by casts
	 order by total_movies desc 
	 limit 10;
```

 
### 15. Categorize the content based on the presence of the keywords 'kill' and 'violence' in the description field. Label content containing these keywords as 'Bad' and all other content as 'Good'. Count how many items fall into each category.
```sql

select 
     case
	    when description like '%kill%'
		      or
		     description like '%violence%'
			then 'bad'
			else 'good'
			end as category,
			count(*) as total 
			from netflix
			group by category;
```

### 16.List all content that has 'International' in the genre
```sql
      SELECT * FROM netflix 
	        WHERE 
			listed_in LIKE '%International%';
			
	```		
   
### 17.Find the oldest movie
```sql
        SELECT * FROM netflix
		WHERE
		type = 'Movie'
		ORDER BY release_year ASC
		LIMIT 1;
```

 ### 18.Count TV shows released after 2018
```sql
   SELECT COUNT(*) FROM netflix
        WHERE 
		type = 'TV Show' AND release_year > 2018;

```
### 19.Find content where director and country are both missing
```sql
   SELECT * FROM netflix
         WHERE director IS NULL
		 AND
		 country IS NULL;
```
### 20.List movies with 'Comedy' genre
```sql
	   SELECT * FROM netflix
	   WHERE
	   type = 'Movie' 
	   AND
	   listed_in LIKE '%Comedies%';
   ```

### 21.Find the maximum release year present in the database
```sql
       SELECT MAX(release_year) FROM netflix;


```
### 22.Group content by 'rating' and count how many items in each
   ```sql
   SELECT rating,
   COUNT(*) 
   FROM netflix
   GROUP BY rating;
   
 ```
### 23.Find all content added in the month of 'January'
```sql
   SELECT * FROM netflix
   WHERE date_added
   LIKE '%January%';
   
   ```
 ### 24.Count distinct countries present in the dataset
```sql
   SELECT COUNT(DISTINCT country) FROM netflix;
   
   ```
### 25.List content where the description contains the word 'love'
```sql

   SELECT * FROM netflix 
   WHERE 
   description ILIKE '%love%';
   
   ```



### created by vemula prasanth

### connect with me:[linkedin](https://www.linkedin.com/in/prasanth-vemula-74702b2b6?utm_source=share_via&utm_content=profile&utm_medium=member_android)




















































