## Further Business Analysis using SQL

## In this blog I will attempt to answer some business questions based on the data I worked on in the data exploration file. 

### Table Initialization
```
create table accenture
(
	datetime date,
	content_id varchar(70),
	reaction_type varchar(30),
	content_type varchar(30),
	category varchar(30),
	sentiment varchar(30),
	score int
)
```
### 1- Write a query to show the number of content posted.
```
select count(content_id) from accenture
```
### 2- Write a query to show the 5 most category and their score.
```
select
   category, count(score)
from accenture
group by 1
order by 2 desc limit 5
```
### 3- Write a query to show reactions with the most popular category.
```
select
   reaction_type, count(*)
from accenture
group by 1
order by 2 desc
```
### 4- List all content posted in the year of 2020.
```
with res as
   (
      select *, extract(year from datetime) as year from accenture
   )
select * from res where year = 2020
```
### 5- Count the number of content in each content type and list them in order from hightest to lowest.
```
select
   content_type, count(content_id) 
from accenture group by 1
order by 2 desc
```
### 6- Write an sql query to show the total count of each sentiment by content type.
```
select
    content_type, sentiment ,count(content_id) as total_count 
from accenture
group by 1,2
order by 1 desc

```
### 7- Write an sql quere to show the 5 most posted reaction type.
```
select
   reaction_type, count(content_id) 
from accenture
group by 1
order by 2 desc
limit 5

```
### 8- Write an sql quere to show all content posted in the last 10 days.
```
with res as(
	select *, extract(day from datetime) as days 
	from accenture )
select * from res
where days >= extract(day from current_date) - 10
```
### 9- Find the most common reaction type for the 5 most populated category.
```
select category, reaction_type from
(
	select
		category, reaction_type,
		rank() over(partition by category order by count(score) desc) as category_type
		from accenture
		group by 1,2
) as temp where category_type = 1 limit 5
```
### 10-  Return the date, content type, reaction type and sentiment of the post with the highest score.
```
select
	datetime, content_type, reaction_type, sentiment, count(score)
from accenture
group by 1,2,3,4
order by 5 desc 
limit 1
```


















   
