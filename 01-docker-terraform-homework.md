## Module 1 Homework
this modile was overdue due to exams and as a beginner it took time to learn and get familiar with docker 

## Question 1. Knowing docker tags
  Which tag has the following text? - *Automatically remove the container when it exits* .
  
  answer : --rm automatically removes the container when it exist.
  
## Question 2. Understanding docker first run 
  What is version of the package *wheel* ?
  command used
```
  docker run -it python:3.9 pip list
```
output:

## Question 3. Count records 

How many taxi trips were totally made on September 18th 2019?
answer : soved it by two ways
first 
```
SELECT COUNT(*)
	FROM yellow_taxi_trips where lpep_pickup_datetime like '2019-09-18%' and lpep_dropoff_datetime like '2019-09-18%';
```
second 
```
SELECT COUNT(*)
FROM yellow_taxi_trips
WHERE SUBSTRING(lpep_pickup_datetime, 1, 10) >= '2019-09-18'
AND SUBSTRING(lpep_pickup_datetime, 1, 10) < '2019-09-19'
AND SUBSTRING(lpep_dropoff_datetime, 1, 10) >= '2019-09-18'
AND SUBSTRING(lpep_dropoff_datetime, 1, 10) < '2019-09-19';
```
output:

## Question 4. Longest trip for each day

Which was the pick up day with the longest trip distance?
answer: solved it by two ways
first
```
WITH max_distance AS (
  SELECT MAX(trip_distance) AS max_distance
  FROM yellow_taxi_trips
)
SELECT lpep_pickup_datetime
FROM yellow_taxi_trips
WHERE trip_distance = (SELECT max_distance FROM max_distance);
```
second
```
SELECT lpep_pickup_datetime from yellow_taxi_trips where trip_distance=(SELECT MAX(trip_distance)
	FROM public.yellow_taxi_trips);
```


