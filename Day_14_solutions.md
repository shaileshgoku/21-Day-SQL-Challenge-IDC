 use hospital;
 
-- Day 14
-- 1. Show all staff members and their schedule information (including those with no schedule entries).

select s.staff_id,s.staff_name,s.role,s.service,ss.week,ss.present from staff s

Left Join staff_schedule ss

on s.staff_id = ss.staff_id; 

![solutions](/images/14.1.PNG)

-- 2. List all services from services_weekly and their corresponding staff (show services even if no staff assigned).

select * from services_weekly sw

Left Join staff s

on sw.service = s.service;

![solutions](/images/14.2.PNG)

	
-- 3. Display all patients and their service's weekly statistics (if available).

select * from patients p

LEFT JOIN services_weekly sw

on p.service = sw.service;

![solutions](/images/14.3.PNG)

/* Daily Challenge: Create a staff utilisation report showing all staff members (staff_id, staff_name, role, service) and the count of weeks they were present
(from staff_schedule). Include staff members even if they have no schedule records. Order by weeks present descending.*/

select s.staff_id,s.staff_name,s.role,s.service, count(ss.week) as week_count

FROM staff s LEFT JOIN staff_schedule ss

on s.staff_id = ss.staff_id

GROUP BY s.staff_id,s.staff_name,s.role,s.service

ORDER BY week_count desc; 

![solutions](/images/14.4.PNG)


=====================================================================

LEFT JOIN
→ Keep everything from the left table.

COUNT(column)
→ Ignore NULL.

COUNT(*)
→ Counts the joined row, even if right-side values are NULL.
