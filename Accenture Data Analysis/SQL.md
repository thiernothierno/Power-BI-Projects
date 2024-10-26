## Further Business Analysis

### In this blog I will attempt to answer some business questions related to the cleaned data I worked on using pandas. 
#### 1- Write a query to show the number of content posted
```
select count(content_id) from accenture
```
#### 2- Write a query to show the 5 most of category and their score
```
select category, count(score)
from accenture
group by 1
order by 2 desc limit 5
```

   
