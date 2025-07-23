
This repository contains an exploratory SQL analysis of the **Netflix Titles Dataset**. The goal is to gain insights into the distribution of content, release patterns, genre trends, and other key metrics using structured queries.

---

## 🧠 Project Objectives

- Understand the overall size and structure of the Netflix content library.
- Analyze the distribution of shows vs movies.
- Explore how content is distributed across years, countries, and directors.
- Identify trends in content additions over time.
- Gain insight into genre popularity and duration metrics.
- Filter and identify records based on specific conditions like region, seasons, and missing data.

---

## 🗂️ Database & Table

- **Database Name**: `NETFLIX`
- **Primary Table**: `TITLES`

This dataset includes fields like:
- `type` (Movie/TV Show)
- `title`
- `director`
- `country`
- `date_added`
- `release_year`
- `rating`
- `duration`
- `listed_in` (Genre categories)

---

## 🧾 SQL Queries Breakdown

### 1. 📦 Total Records
```sql
SELECT COUNT(*) AS TOTAL_RECORDS FROM TITLES;
````

Counts the total number of records available in the `TITLES` table.

---

### 2. 🎬 Distribution by Content Type

```sql
SELECT TYPE, COUNT(*) FROM TITLES GROUP BY TYPE;
```

Breaks down the number of Movies vs TV Shows on the platform.

---

### 3. 🔢 Rating Distribution

```sql
SELECT RATING, COUNT(*) FROM TITLES GROUP BY RATING;
```

Analyzes how content is distributed across various content ratings (e.g., TV-MA, PG, R, etc.).

---

### 4. 📅 Content by Release Year

```sql
SELECT RELEASE_YEAR, COUNT(*) FROM TITLES GROUP BY RELEASE_YEAR;
```

Shows how many titles were released each year.

---

### 5. 🎥 Top 10 Most Common Directors

```sql
SELECT DIRECTOR, COUNT(*) FROM TITLES GROUP BY DIRECTOR ORDER BY COUNT DESC LIMIT 10;
```

Reveals the most frequently featured directors in the catalog.

---

### 6. 🌍 Top 10 Content-Producing Countries

```sql
SELECT COUNTRY, COUNT(*) FROM TITLES GROUP BY COUNTRY ORDER BY COUNT DESC LIMIT 10;
```

Identifies which countries contribute the most content.

---

### 7. 🗓️ Monthly Additions Trend

```sql
SELECT DATE_FORMAT(STR_TO_DATE(DATE_ADDED,'%B %d, %Y'), '%Y-%m') AS MONTH, COUNT(*) 
FROM TITLES GROUP BY MONTH;
```

Analyzes the number of titles added to Netflix each month.

---

### 8. 📆 Yearly Additions Trend

```sql
SELECT YEAR(STR_TO_DATE(DATE_ADDED, '%B %d, %Y')) AS YEAR, COUNT(*) FROM TITLES GROUP BY YEAR;
```

Shows how the library has grown year-over-year.

---

### 9. 🎭 Total Number of Dramas

```sql
SELECT COUNT(*) FROM TITLES WHERE LISTED_IN LIKE '%DRAMAS%';
```

Counts how many titles fall under the Drama category.

---

### 10. ⏱️ Average Movie Duration

```sql
SELECT AVG(CAST(SUBSTRING_INDEX(DURATION,' ',1) AS UNSIGNED)) AS AVERAGE_DURATION 
FROM TITLES WHERE DURATION REGEXP '^[0-9]+ MIN$';
```

Calculates the average duration of movies in minutes.

---

### 11. ❌ Records Without Director Information

```sql
SELECT COUNT(*) FROM TITLES WHERE DIRECTOR = '';
```

Finds titles missing director data.

---

### 12. 🆕 Recently Released Content (Last 5 Years)

```sql
SELECT * FROM TITLES WHERE RELEASE_YEAR >= YEAR(CURDATE()) - 5;
```

Filters content released in the past 5 years.

---

### 13. 🇮🇳 Indian Content on Netflix

```sql
SELECT TYPE, TITLE FROM TITLES WHERE COUNTRY = 'INDIA';
```

Displays Indian content and its type (Movie/TV Show).

---

### 14. 📺 Shows with Seasons

```sql
SELECT * FROM TITLES WHERE DURATION LIKE '%SEASONS%';
```

Fetches TV Shows that include season-based duration.

---

### 15. ➕ Shows with More Than 2 Seasons

```sql
SELECT * FROM TITLES 
WHERE DURATION LIKE '%SEASONS%' 
AND CAST(SUBSTRING_INDEX(DURATION, ' ', 1) AS UNSIGNED) > 2;
```

Isolates long-running TV Shows with more than two seasons.

---

## 📈 Insights You Can Gain

* How fast Netflix is expanding its content.
* Which countries or genres are dominating the library.
* The balance between TV Shows and Movies.
* Popular directors and their frequency.
* Genre trends like Dramas or Kids content.
* How much time a user might spend on an average movie.

**Email**: *mahek456shrivastava@gmail.com*
**GitHub**: https://github.com/Mahek45600 
