#1. Count the total number of patients in the hospital.

SELECT COUNT(*) AS total_count

FROM patients;

![solutions](/images/5.1.PNG)




# 2. Calculate the average satisfaction score of all patients.

SELECT avg(satisfaction) as average_satisfaction_score

FROM patients;

![solutions](/images/5.2.PNG)



# 3. Find the minimum and maximum age of patients.

SELECT min(age) as minimum_age,
       
max(age) as maximum_age

FROM patients;

![solutions](/images/5.3.PNG)




# Question : Calculate the total number of patients admitted, total patients refused, and the average patient
#			 satisfaction across all services and weeks. Round the average satisfaction to 2 decimal places.
  
SELECT SUM(patients_admitted) AS total_admitted, 
       SUM(patients_refused) AS total_refused, 
       ROUND(AVG(patient_satisfaction), 2) AS average_satisfaction

FROM services_weekly; 

-- since it is overall result asked. not per result asked in question. no group by is needed

/* don't use group by when question contains:
Whenever you see phrases like:

overall

across all

entire hospital

total hospital

all weeks

all services

Ask yourself:

"Do I need one result or multiple results?"

If the answer is one result, then you usually don't need GROUP BY.

use group by:

Per service

Per week

Per department

Per customer

Per city

If the question doesn't ask per something, then pause before adding GROUP BY. */

![solutions](/images/5.4.PNG)
