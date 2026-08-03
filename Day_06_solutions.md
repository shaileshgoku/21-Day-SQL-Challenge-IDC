# 1. Count the number of patients by each service.

SELECT service, 

count(name) as no_of_patients 

FROM patients

GROUP BY service;

![solutions](/images/6.1.PNG)



# 2. Calculate the average age of patients grouped by service.

SELECT service,

round(avg(age),0) as avg_age

FROM patients

GROUP BY service;

![solutions](/images/6.2.PNG)


# 3. Find the total number of staff members per role.

SELECT role,

count(staff_name) as total_staff

FROM staff

GROUP BY role;

![solutions](/images/6.3.PNG)



#Question: For each hospital service, calculate the total number of patients admitted, 
#          total patients refused, and the admission rate (percentage of requests that were admitted). 
#          Order by admission rate descending.
SELECT service,

SUM(patients_admitted) AS total_admitted,

SUM(patients_refused) AS total_refused,

ROUND(

SUM(patients_admitted) * 100.0

/ SUM(patients_request),

2

) AS admission_rate

FROM services_weekly

GROUP BY service

ORDER BY admission_rate DESC;

![solutions](/images/6.4.PNG)
