
# HackerRank SQL Practice Solutions

This repository contains solutions to various SQL problems from HackerRank.

---

## QUERY 1
**Problem:** Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from the STATION table. The result **must not contain duplicates**.

**Solution:**
```sql
SELECT DISTINCT city 
FROM station
WHERE city LIKE 'a%' 
   OR city LIKE 'e%' 
   OR city LIKE 'i%' 
   OR city LIKE 'o%' 
   OR city LIKE 'u%';
```

---

## QUERY 2
**Problem:** Query the list of CITY names ending with vowels (a, e, i, o, u). No duplicates.

**Solution:**
```sql
SELECT DISTINCT city 
FROM station
WHERE city LIKE '%a' 
   OR city LIKE '%e' 
   OR city LIKE '%i' 
   OR city LIKE '%o' 
   OR city LIKE '%u';
```

---

## QUERY 3
**Problem:** Query CITY names where both the first and last characters are vowels.

**Solution:**
```sql
SELECT DISTINCT city
FROM station
WHERE LOWER(LEFT(city, 1))  IN ('a','e','i','o','u')
  AND LOWER(RIGHT(city, 1)) IN ('a','e','i','o','u');
```

---

## QUERY 4
**Problem:** Find names of students with marks greater than 75.  
Sort by last three characters of the name, then by ID if there's a tie.

**Solution:**
```sql
SELECT name 
FROM students
WHERE marks > 75
ORDER BY RIGHT(name, 3), id;
```

---

## QUERY 5
**Problem:** Print names of employees with salary > 2000 and experience < 10 months.  
Sort by employee_id.

**Solution:**
```sql
SELECT name 
FROM employee
WHERE salary > 2000 
  AND months < 10
ORDER BY employee_id;
```

---

## QUERY 7
**Problem:** Print a pattern P(20) with decreasing stars per line.

**Solution:**
```sql
SET @number = 21;
SELECT REPEAT('* ', @number := @number - 1) 
FROM information_schema.tables;
```

---

## QUERY 8
**Problem:** Find maximum total earnings (salary × months) and the number of employees earning it.

**Solution:**
```sql
SELECT (salary * months) AS earning, 
       COUNT(*) AS c
FROM employee 
WHERE (salary * months) = (
    SELECT MAX(salary * months) 
    FROM employee
)
GROUP BY salary * months;
```

---

## QUERY 9
**Problem:** Find the sum of the population of all cities where the continent is 'Asia'.  
Tables: CITY and COUNTRY

**Solution:**
```sql
SELECT SUM(city.population) 
FROM city
INNER JOIN country
    ON city.countrycode = country.code
WHERE country.continent = 'Asia';
```

## QUERY 10:
### Problem Description  
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

**Note:** CITY.CountryCode and COUNTRY.Code are matching key columns.

### Solution  
```sql
SELECT city.name 
FROM city
INNER JOIN country
ON city.CountryCode = country.Code
WHERE country.continent = 'Africa';

## QUERY 11: AVERAGE CITY POPULATION BY CONTINENT (ROUNDED DOWN)

### PROBLEM DESCRIPTION  
Given the CITY and COUNTRY tables, query the names of all the continents (`COUNTRY.Continent`) and their respective average city populations (`CITY.Population`) rounded down to the nearest integer.

**Note:** `CITY.CountryCode` and `COUNTRY.Code` are matching key columns.

### SOLUTION  
```sql
SELECT country.continent, FLOOR(AVG(city.population)) 
FROM country
INNER JOIN city
ON city.CountryCode = country.Code
GROUP BY country.continent;
