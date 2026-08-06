use hospital;

# 1. Categorise patients as 'High', 'Medium', or 'Low' satisfaction based on their scores.

SELECT name,satisfaction,

(CASE

WHEN satisfaction > 80 THEN "High"

WHEN satisfaction >50 THEN "Medium"

ELSE "Low" 

END) as category 

FROM patients;

![solutions](/images/10.1.PNG)


# 2. Label staff roles as 'Medical' or 'Support' based on role type

SELECT distinct role,

(CASE

WHEN role = "nursing_assistant" THEN "Support"

ELSE "Medical"

END) as role_type  

FROM staff;

![solutions](/images/10.2.PNG)
	
    
# 3. Create age groups for patients (0-18, 19-40, 41-65, 65+).

SELECT name, age,

CASE

WHEN age >= 65 THEN '65+'

WHEN age >= 41 THEN '41-65'

WHEN age >= 19 THEN '19-40'

ELSE '0-18'

END as age_groups

FROM patients;

![solutions](/images/10.3.PNG)

# Question: Create a service performance report showing service name, total patients admitted, and 
#           a performance category based on the following: 'Excellent' if avg satisfaction >= 85, 'Good' 
#           if >= 75, 'Fair' if >= 65, otherwise 'Needs Improvement'. Order by average satisfaction descending.

SELECT service, sum(patients_admitted) as total_admitted, avg(patient_satisfaction) as average_satisfaction,

CASE

WHEN avg(patient_satisfaction) >= 85 THEN 'Excellent'

WHEN avg(patient_satisfaction) >= 75 THEN 'Good'

WHEN avg(patient_satisfaction) >= 65 THEN 'Fair'

ELSE 'Needs Improvement'

END as performance_category

FROM services_weekly

GROUP BY service

ORDER BY average_satisfaction desc;

![solutions](/images/10.4.PNG)

=======================================================================

CASE statements are evaluated
from top to bottom.

SQL stops at the FIRST matching condition.

Example

CASE

WHEN age >= 65 THEN 'Senior'

WHEN age >= 18 THEN 'Adult'

ELSE 'Minor'

END

Age = 70

↓

Checks:

age >= 65

TRUE

↓

Stops.

Rule:

Write CASE conditions
from the most restrictive
(or highest range)
to the lowest range.

================================================================

Whenever a requirement gives ranges like:

0-18
19-40
41-65
65+

Check the boundary values carefully.

Ask yourself:

Where does 18 go?
Where does 19 go?
Where does 40 go?
Where does 41 go?
Where does 65 go?

Most SQL mistakes happen because of
using > instead of >=
or < instead of <=.

Always test the boundary values.


