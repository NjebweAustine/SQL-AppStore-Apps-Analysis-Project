# SQL-AppStore-Apps-Analysis-Project

## Project Overview

This project covers information about apps available in the App Store. There are two datasets, one of which is the app description because there is a lot of value to derive in terms of user interface and how an app is regarded on the market.


## Stakeholders

My clients in this project are app developers and businesses who need data-driven insights to decide what type of app to build. They are seeking answers to the following questions

1. What app categories are the most popular?
2. What price should they set?
3. How can user ratings be maximized?

### Data Sources

There are two datasets used in this project. The primary dataset is the "appleStore.csv" file which provides information such as app names, sizing bytes, ratings, and number of supported languages, among others. 
The second dataset is the "appleStore_Description.csv" file which provides an overview description of apps such as how an app is perceived by users. [Download here]. (https://drive.google.com/drive/folders/14O9xB8N1gXN_67ouphImQkvpzyitmTfR)


### Tools

- SQLite- Exploratory Data Analysis. [Get it here]. (https://sqliteonline.com/)
- PowerBI- To create a report

## Data Preparation
In the initial data preparation, I had performed the following tasks

1. Data loading
2. Joining the 5 separate tables using the UNION ALL function to have one uniform dataset

## Exploratory Data Analysis

A process that allows us to understand the nature and structure of the data. Also reveals any issues in the data, such as missing or inconsistent data, before further analysis. This increases the accuracy of the data, hence more relevant problem-solving insights, and also saves a lot of time in the later stages of the analysis.

### Key areas

1. Checking the number of unique apps in both tables
```SQL
SELECT COUNT(DISTINCT id) AS UniqueAppIds
FROM AppleStore

SELECT COUNT(DISTINCT id) AS UniqueAppIds
FROM appleStore_description_combined
```
2. Checking for any missing values in key fields
```SQL
SELECT COUNT(*) AS Missingvalues
FROM AppleStore
WHERE track_name is null OR user_rating IS null OR prime_genre IS null

SELECT COUNT(*) AS Missingvalues
FROM appleStore_description_combined
WHERE app_desc is null
```

3. Finding out the number of apps per genre
```SQL
SELECT prime_genre, COUNT(*) AS NumApps
FROM AppleStore
GROUP BY prime_genre
ORDER BY NumApps DESC
```

4. Getting an overview of the apps’ ratings
```SQL
SELECT MIN(user_rating) AS MinRating,
       MAX(user_rating) AS MaxRating,
       AVG(user_rating) AS AvgRating
FROM AppleStore
```

## Analysis

•	Determine whether paid apps have higher ratings than free apps

•	Check if apps with more languages have a higher rating

•	Check genres with low ratings

•	Check if there is a correlation between the app description length and the user rating

•	Check Top Rated apps for each category

### Interesting code/features
```SQL
--Check Top Rated apps for each category

SELECT
    prime_genre,
    track_name,
    user_rating
FROM (
    SELECT
        prime_genre,
        track_name,
        user_rating,
        RANK() OVER (PARTITION BY prime_genre ORDER BY user_rating DESC, rating_count_tot DESC) AS rank
    FROM AppleStore
) AS a
WHERE a.rank = 1;
```
---

## Results and their Recommendations
Based on the analysis done, the following are the results of our major questions and their respective recommendations;

•	Paid apps have better ratings- The user gets more value from a paid app, hence getting more engagement. Clients should consider charging an amount for the app.

•	Apps supporting between 10 and 30 languages have better ratings. The language choice matters too.

•	Finance and book apps have lower ratings. This means that the user needs are not being met, hence representing an opportunity to create an app with adjustments for user needs that will allow higher ratings and market dominance.

•	Apps with a longer description have better ratings. Users appreciate a clear understanding of an app’s full capabilities before downloading it. A well-structured description sets a clear expectation from the users, equating to user satisfaction.

•	A new app should aim for an average rating of 3.5 and above.

•	Games and Entertainment apps face more competition. There is a saturation of apps in the games and entertainment space, therefore the developers must be willing to face stiff competition.

### References
- [Google Scholar Articles]. (https://doi.org/10.1002/asi.23932)

🖥️
💻





