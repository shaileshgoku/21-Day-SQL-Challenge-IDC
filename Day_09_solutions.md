use hospital;

# 1. Extract the year from all patient arrival dates.

SELECT YEAR(arrival_date) AS arrival_year

FROM patients;

![solutions](/images/9.1.PNG)


# 2. Calculate the length of stay for each patient (departure_date - arrival_date).

SELECT name,

DATEDIFF(departure_date, arrival_date) AS length_of_stay

FROM patients;

![solutions](/images/9.2.PNG)

# 3. Find all patients who arrived in a specific month.

SELECT name, monthname(arrival_date) as arrived_date 

FROM patients;

![solutions](/images/9.3.PNG)

# Question: Calculate the average length of stay (in days) for each service, 
#           showing only services where the average stay is more than 7 days. 
#			Also show the count of patients and order by average stay descending.
WITH cte AS (

SELECT name,

service,

DATEDIFF(departure_date, arrival_date) AS length_of_stay

FROM patients

)

SELECT service,

COUNT(*) AS patients_count,

AVG(length_of_stay) AS avg_stay_length

FROM cte

GROUP BY service

HAVING AVG(length_of_stay) > 7

ORDER BY avg_stay_length DESC;

![solutions](/images/9.4.PNG)

=================================================================================

When working with dates,

❌ Don't calculate days manually using

(MONTH(end)-MONTH(start))*30
+
(DAY(end)-DAY(start))

Months have:

28 days
29 days
30 days
31 days

Leap years also exist.

✅ Use built-in date functions.

Examples (MySQL):

DATEDIFF(end_date, start_date)

DATE_ADD()

DATE_SUB()

TIMESTAMPDIFF()

Rule:

Whenever SQL provides a built-in date function,
prefer it over manual calculations.


