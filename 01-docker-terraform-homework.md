## Module 1 Homework
this module was overdue due to exams and as a beginner it took time to learn and get familiar with docker 

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
![alt text](https://github.com/faizeraza/de-cohort-2024/blob/main/qn2.png)

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
![alt text](https://github.com/faizeraza/de-cohort-2024/blob/main/qn3.png)

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

output:
![alt text](https://github.com/faizeraza/de-cohort-2024/blob/main/qn4.png)

## Question 5. Three biggest pick up Boroughs

Consider lpep_pickup_datetime in '2019-09-18' and ignoring Borough has Unknown

Which were the 3 pick up Boroughs that had a sum of total_amount superior to 50000?
```
SELECT z."Borough" AS total_amount
FROM zones AS z
INNER JOIN yellow_taxi_trips AS yt ON z."LocationID" = yt."PULocationID"
GROUP BY z."Borough" having sum(yt."total_amount")>50000 limit 3;
```
output:
![alt text](https://github.com/faizeraza/de-cohort-2024/blob/main/qn5.png)
### Question 6. Largest tip

For the passengers picked up in September 2019 in the zone name Astoria which was the drop off zone that had the largest tip? We want the name of the zone, not the id.

```
WITH boroughinzone as(
	SELECT "LocationID" FROM zones where "Zone" like 'Astoria'
),
zoneofmaxtip as (
	SELECT "DOLocationID" FROM yellow_taxi_trips as ytt WHERE SUBSTRING(lpep_pickup_datetime, 1, 7) >= '2019-09' 
	AND "PULocationID" = (SELECT "LocationID" FROM boroughinzone) ORDER BY tip_amount DESC LIMIT 1
)
select "Zone" from zones where "LocationID" = (SELECT "DOLocationID" FROM zoneofmaxtip);
```
![alt text](https://github.com/faizeraza/de-cohort-2024/blob/main/qn6.png)

