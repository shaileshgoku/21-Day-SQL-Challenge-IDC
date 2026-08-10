use hospital;

# 1. Join patients and staff based on their common service field (show patient and staff who work in same service).

select * from patients p

join staff s

on p.service = s.service;

![solutions](/images/13.1.PNG)

# 2. Join services_weekly with staff to show weekly service data with staff information.

select * from services_weekly sw

join staff s

on sw.service = s.service;

![solutions](/images/13.2.PNG)
	
# 3. Create a report showing patient information along with staff assigned to their service.

select * from patients p

join staff s

on p.service = s.service;

![solutions](/images/13.3.PNG)

# Question: Create a comprehensive report showing patient_id, patient name, age, service, and the total number 
#           of staff members available in their service. Only include patients from services that have
#           more than 5 staff members. Order by number of staff descending, then by patient name.

select p.patient_id,p.name,p.age,p.service,count(s.staff_name) as staff_count

from patients p

join staff s

on p.service = s.service

group by p.service,p.patient_id,p.name,p.age

having count(s.staff_name) > 5

order by staff_count desc, p.name asc;

![solutions](/images/13.4.PNG)


====================================================================================

JOIN
↓
Can multiply rows

GROUP BY
↓
Can collapse those rows

COUNT()
↓
Can measure the multiplied matches
