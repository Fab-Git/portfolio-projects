# Data Analysis of RSVP Movies

## Project Overview
This project focuses on analyzing a comprehensive movie dataset using **SQL** to extract actionable insights for **RSVP Movies**, a production company. By leveraging SQL queries, I explored patterns related to movie production, genre trends, ratings, and more. The findings provide data-driven recommendations to guide future decisions in production, casting, and partnerships.

---

## Entity-Relationship Diagram (ERD)
The ERD represents the relationships between key entities in the dataset, including movies, genres, actors, directors, and ratings.

---

## Key Objectives
1. Understand the distribution of movies by year, month, country, and genre.
2. Identify top-performing genres, directors, actors, and actresses based on ratings and votes.
3. Analyze production houses to recommend partnerships based on historical success.
4. Explore trends in multilingual movies and classify movies by performance (e.g., super hit, hit, flop).
5. Provide strategic insights for production planning, talent hiring, and genre selection.

---

## Key Queries and Insights

### 1. **Schema Exploration & Row Count**
```sql
SELECT 'director_mapping' AS table_name, COUNT(*) AS row_count FROM director_mapping
UNION ALL
SELECT 'genre' AS table_name, COUNT(*) AS row_count FROM genre
UNION ALL
SELECT 'movie' AS table_name, COUNT(*) AS row_count FROM movie
UNION ALL
SELECT 'names' AS table_name, COUNT(*) AS row_count FROM names
UNION ALL
SELECT 'ratings' AS table_name, COUNT(*) AS row_count FROM ratings
UNION ALL
SELECT 'role_mapping' AS table_name, COUNT(*) AS row_count FROM role_mapping
ORDER BY row_count DESC;

**Insight:** The dataset’s largest table, names, contains over 25,000 records, providing a comprehensive view of actors, directors, and movies.

### 2. **Handling Missing Data in the Movie Table**
```sql
SELECT COUNT(*) AS total_rows,
    SUM(CASE WHEN id IS NULL THEN 1 ELSE 0 END) AS id_nulls,
    SUM(CASE WHEN title IS NULL THEN 1 ELSE 0 END) AS title_nulls,
    SUM(CASE WHEN year IS NULL THEN 1 ELSE 0 END) AS year_nulls,
    SUM(CASE WHEN date_published IS NULL THEN 1 ELSE 0 END) AS date_published_nulls,
    SUM(CASE WHEN duration IS NULL THEN 1 ELSE 0 END) AS duration_nulls,
    SUM(CASE WHEN country IS NULL THEN 1 ELSE 0 END) AS country_nulls,
    SUM(CASE WHEN worlwide_gross_income IS NULL THEN 1 ELSE 0 END) AS worldwide_gross_income_nulls,
    SUM(CASE WHEN production_company IS NULL THEN 1 ELSE 0 END) AS production_company_nulls
FROM movie;

**Insight:** Columns like worlwide_gross_income and production_company have significant missing data, requiring cleaning for accurate analysis.

### 3. **Trends in Movie Releases**
```sql
SELECT year, COUNT(id) 
FROM movie 
GROUP BY year;

SELECT MONTH(date_published) AS month, COUNT(id) 
FROM movie 
GROUP BY month 
ORDER BY month;

**Insight:** March is the most active month for movie releases, providing insights into optimal release schedules.

### 4. **Genre Distribution & Top Genres**

**Top Genre Identification**
```sql
    SELECT genre, COUNT(movie_id) AS genre_count
    FROM genre
    GROUP BY genre
    ORDER BY genre_count DESC
    LIMIT 1;

**Insight:** The Drama genre has the highest number of movies produced.

**Movies with Multiple Genres**
```sql
SELECT COUNT(*) 
FROM (
    SELECT movie_id, COUNT(movie_id) AS movie_genre_count
    FROM genre
    GROUP BY movie_id
    HAVING movie_genre_count = 1
) AS mv;

**Insight:** Over 3,000 movies have only one genre, indicating a trend toward genre-specific storytelling.

### 5. **Top Performers by Ratings**

**Top 10 Movies Based on Ratings**
```sql
    SELECT title, avg_rating, RANK() OVER(ORDER BY avg_rating DESC) AS movie_rank
    FROM movie m
    INNER JOIN ratings r ON r.movie_id = m.id
    LIMIT 10;

**Top Directors in Top Genres (Average Rating > 8)**
```sql
WITH top_genres AS (
    SELECT genre, COUNT(gn.movie_id) AS movie_count
    FROM genre gn
    INNER JOIN ratings rt ON rt.movie_id = gn.movie_id
    WHERE rt.avg_rating > 8
    GROUP BY genre
    ORDER BY COUNT(gn.movie_id) DESC
)
SELECT nm.name, COUNT(m.id) AS movie_count
FROM movie m
INNER JOIN ratings r ON r.movie_id = m.id
INNER JOIN genre g ON g.movie_id = m.id
INNER JOIN role_mapping rm ON rm.movie_id = m.id
INNER JOIN names nm ON nm.id = rm.name_id
WHERE g.genre IN (SELECT genre FROM top_genres)
AND r.avg_rating > 8
GROUP BY nm.name
ORDER BY movie_count DESC
LIMIT 3;

**Insight:** Highly rated directors and actors bring strong box office appeal, guiding talent hiring decisions.

### 6. **Analyzing Production House Success**

**Top 3 Production Houses Based on Votes**
```sql
SELECT production_company, SUM(r.total_votes) AS vote_count, 
    RANK() OVER (ORDER BY SUM(r.total_votes) DESC) AS prod_comp_rank
FROM movie m
INNER JOIN ratings r ON r.movie_id = m.id
GROUP BY production_company
ORDER BY vote_count DESC;

**Insight:** Production houses with high audience engagement are ideal candidates for partnerships.

### 7. **Movie Performance Analysis**

**Classifying Thriller Movies by Performance**
```sql
SELECT m.title, r.avg_rating, 
       CASE 
           WHEN r.avg_rating > 8 THEN 'Superhit movies'
           WHEN r.avg_rating BETWEEN 7 AND 8 THEN 'Hit movies'
           WHEN r.avg_rating BETWEEN 5 AND 7 THEN 'One-time-watch movies'
           ELSE 'Flop movies'
       END AS movie_type
FROM movie m
INNER JOIN ratings r ON r.movie_id = m.id
INNER JOIN genre g ON g.movie_id = m.id
WHERE g.genre = 'Thriller'
ORDER BY r.avg_rating DESC;

**Insight:** Classifies thriller movies into categories like "Superhit" or "Flop" based on average ratings, guiding future investments in this genre.

## Technologies Used
- **SQL**: Extracted, transformed, and analyzed data.
- **Entity-Relationship Diagram (ERD)**: Visualized relationships between key entities.
- **Window Functions**: Used for ranking, calculating running totals, and deriving insights.

---

## Conclusion
This analysis provided **RSVP Movies** with actionable insights into:
- Genre trends.
- Top performers (actors, directors, and production houses).
- Production house success.
