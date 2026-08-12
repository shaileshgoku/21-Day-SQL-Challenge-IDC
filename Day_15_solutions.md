# 1. Join patients, staff, and staff_schedule to show patient service and staff availability.

SELECT p.patient_id,

p.name AS patient_name,

s.service,

s.staff_id,

s.staff_name,

ss.week,

ss.present

FROM patients p

JOIN staff s

ON p.service = s.service

JOIN staff_schedule ss

ON s.staff_id = ss.staff_id;

![solutions](/images/15.1.PNG)


# 2. Combine services_weekly with staff and staff_schedule for comprehensive service analysis.

SELECT sw.week,

sw.service,

sw.patients_admitted,

sw.patients_refused,

s.staff_id,

s.staff_name,

s.role,

ss.present

FROM services_weekly sw

JOIN staff s

ON sw.service = s.service

JOIN staff_schedule ss

ON s.staff_id = ss.staff_id

AND sw.week = ss.week;

![solutions](/images/15.2.PNG)

# 3. Create a multi-table report showing patient admissions with staff information.

SELECT p.patient_id,

p.name AS patient_name,

p.service,

s.staff_id,

s.staff_name,

s.role

FROM patients p

JOIN staff s

ON p.service = s.service;

![solutions](/images/15.3.PNG)


# Question: Create a comprehensive service analysis report for week 20 showing: service name, total patients
#           admitted that week, total patients refused, average patient satisfaction, count of staff assigned
#           to service, and count of staff present that week. Order by patients admitted descending.

WITH weekly_stats AS (

SELECT service,

SUM(patients_admitted) AS total_admitted,

SUM(patients_refused) AS total_refused,

AVG(patient_satisfaction) AS avg_patient_satisfaction

FROM services_weekly

WHERE week = 20

GROUP BY service

),

staff_count AS (

SELECT service,

COUNT(*) AS staff_assigned

FROM staff

GROUP BY service

),

staff_present AS (

SELECT service,

COUNT(DISTINCT staff_id) AS staff_present

FROM staff_schedule

WHERE week = 20

AND present = 1

GROUP BY service

)

SELECT ws.service,

ws.total_admitted,

ws.total_refused,

ws.avg_patient_satisfaction,

sc.staff_assigned,

COALESCE(sp.staff_present, 0) AS staff_present

FROM weekly_stats ws

LEFT JOIN staff_count sc

ON ws.service = sc.service

LEFT JOIN staff_present sp

ON ws.service = sp.service

ORDER BY ws.total_admitted DESC;

![solutions](/images/15.4.PNG)
