## Further Business Analysis

### In this blog I will attempt to answer some business questions related to the cleaned data I worked on using pandas. 
#### 1- Write a query to show the number of content posted
```
select count(content_id) from accenture
```
#### 2- Write a query to show the 5 most category and their score
```
select
   category, count(score)
from accenture
group by 1
order by 2 desc limit 5
```
#### 3- Write a query to show reactions with the most popular category
```
select
   reaction_type, count(*)
from accenture
group by 1
order by 2 desc
```
### 4- List all content posted in the year of 2020
```
with res as
   (
      select *, extract(year from datetime) as year from accenture
   )
select * from res where year = 2020
```
   
