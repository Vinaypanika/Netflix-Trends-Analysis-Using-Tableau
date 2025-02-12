# Netflix-Trends-Analysis-Using-Tableau

### Netflix Trends Analysis Dashboard using Tableau. 

This dashboard offers an interactive and engaging way to explore the world of Netflix. Here are some highlights:


### 🌟 Interactive Exploration: 

Seamlessly navigate the Netflix landscape with a thoughtfully designed Tableau dashboard, providing an immersive user experience.
### 📊 Comprehensive Data Analysis: 

Dive deep into key details such as show ID, type, title, director, cast, country, date added, release year, rating, duration, and listed genres. This allows for a thorough understanding of Netflix content.
### 🌍 Global Insights: 


Discover the global distribution of Netflix content by exploring country-wise trends, offering a nuanced understanding of the platform's international reach.
### 🎥 Top Genre Showcase: 

Identify and explore the top 10 genres, offering a quick overview of the most popular content categories on Netflix.
### ⭐ Ratings Dynamics:

Visualize rating distribution to grasp audience preferences and ensure a comprehensive view of content quality.
### 📝 Engaging Descriptions:

Enhance user engagement with detailed descriptions for each movie and TV show, adding depth to the exploration experience.

# Netflix Data Analysis - SQL Queries

## Basic SQL Queries

### 1. Retrieve all columns from the dataset
```sql
select * from netflix;
```

### 2. Count the Number of Records
```sql
select count(*) as number_of_records from netflix;
```

### 3. Find the unique types of content (Movies/TV Shows)
```sql
select distinct type from netflix;
```

### 4. Retrieve all movies released in 2020
```sql
select title from netflix
where release_year = 2020;
```

### 5. Get the top 5 directors with the most titles
```sql
select top 5 director,count(*) as Number_of_titles
from netflix
where director is not null
group by director
order by count(*) desc;
```

### 6. Find the number of movies and TV shows separately
```sql
select type, count(*) Total_number from netflix
group by type;
```

### 7. Find the average duration of movies
```sql
select avg(cast(replace(duration, 'min',' ' )as int)) as average_duration
from netflix
where type = 'Movie' and duration is not null;
```

### 8. Find the top 5 countries with the most Netflix content
```sql
select top 5 country,count(*) as Total_content
from netflix
where country is not null
group by country
order by count(*) desc;
```

### 9. Find the number of titles added per year
```sql
select release_year, count(*) as title_added
from netflix
where release_year is not null
group by release_year
order by release_year desc;
```

### 10. Find the percentage of Movies vs TV Shows
```sql
select type, count(*)*100.0/(select count(*) from netflix) as Percentage
from netflix
group by type;
```

### 11. Find the top genres with the highest number of titles
```sql
with cte_genre as(
	select trim(value) as genre from netflix
	cross apply string_split(listed_in, ','))
select top 5 genre, count(*) as total_titles
from cte_genre
group by genre
order by count(*) desc;
```

### 12. Find the top 5 most frequent actors in Netflix content
```sql
with cte_actor as (
	select trim(value) as actor from netflix
	cross apply string_split(cast,','))
select top 5 actor,count(*) as frequency
from cte_actor
group by actor
order by count(*) desc;
```

### 13. Find the most common release month for Netflix titles
```sql
select datename(month,date_added) as month, count(*) as Total_title
from netflix
where datename(month,date_added) is not null
group by datename(month,date_added)
order by count(*) desc;
```

### 14. Find movies with the longest duration
```sql
select title,duration from netflix
where type = 'movie' and duration is not null
order by cast(replace(duration,'min','') as int) desc;
```

### 15. Find the total number of TV Shows with Seasons count distribution
```sql
select duration, count(*) as total_show
from netflix
where type = 'tv show'
group by duration
order by count(*) desc;
```

### 16. Identify the country with the highest number of TV Shows
```sql
with cte_country as (
	select trim(value) as single_country,count(*) as total_count
	from netflix
	cross apply string_split(country,',')
group by trim(value))
select single_country, total_count
from cte_country
order by total_count desc;
```

### 17. Find the director who has directed the most content for Netflix
```sql
with cte_director as (
	select trim(value) as director, count(*) as total_count
	from netflix
	cross apply string_split(director,',')
	group by trim(value))
select director,total_count
from cte_director
order by total_count desc;
```

### 18. Find the earliest and latest release years in the dataset
```sql
select min(release_year) as earliest_release, max(release_year) as latest_release
from netflix;
```

### 19. Find the year with the highest number of content added
```sql
select top 1 release_year, count(*) as total_count
from netflix
where release_year is not null
group by release_year
order by count(*) desc;
```

### 20. Get a list of movies that belong to multiple genres
```sql
select type, listed_in
from netflix
where type = 'movie' and charindex(',',listed_in)>0;
```

## 📞 Contact

If you have any questions or want to connect, feel free to reach out:

- 📧 Email: [vinaypanika@gmail.com](mailto:vinaypanika@gmail.com)
- 💼 LinkedIn: [Vinay Kumar Panika](https://www.linkedin.com/in/vinaykumarpanika)
- 📂 GitHub: [VinayPanika](https://github.com/Vinaypanika)
- 🌐 Portfolio: [Visit My Portfolio](https://sites.google.com/view/vinaykumarpanika/home)
- 📞 Mobile: [+91 7415552944](tel:+917415552944)
