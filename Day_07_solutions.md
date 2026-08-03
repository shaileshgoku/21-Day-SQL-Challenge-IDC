# 1. Find services that have admitted more than 500 patients in total.

SELECT service,

sum(patients_admitted) as total_admitted

FROM services_weekly

GROUP BY service

HAVING sum(patients_admitted) > 500;

![solutions](/images/7.1.PNG)

# 2. Show services where average patient satisfaction is below 75.

SELECT service,

avg(patient_satisfaction) as patient_satisfaction

FROM services_weekly

GROUP BY service

HAVING avg(patient_satisfaction) < 75;

![solutions](/images/7.2.PNG)

# 3. List weeks where total staff presence across all services was less than 50.

SELECT week,

SUM(present) AS total_staff_presence

FROM staff_schedule

GROUP BY week

HAVING SUM(present) < 50;

![solutions](/images/7.3.PNG)

# Question: Identify services that refused more than 100 patients in total and had an average patient 
#			satisfaction below 80. Show service name, total refused, and average satisfaction.

SELECT service,

sum(patients_refused) as total_refused,

avg(patient_satisfaction) aS avg_satisfaction

FROM services_weekly

GROUP BY service

HAVING sum(patients_refused) > 100 and avg(patient_satisfaction) < 80;

![solutions](/images/7.4.PNG)
