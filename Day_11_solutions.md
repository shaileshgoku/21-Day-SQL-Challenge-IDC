use hospital;

# 1. List all unique services in the patients table.

SELECT DISTINCT service 

FROM patients;

![solutions](/images/11.1.PNG)

# 2. Find all unique staff roles in the hospital.

SELECT DISTINCT role 

FROM staff;

![solutions](/images/11.2.PNG)



# 3. Get distinct months from the services_weekly table.

SELECT DISTINCT month 

FROM services_weekly;

![solutions](/images/11.3.PNG)


# Question: Find all unique combinations of service and event type from the services_weekly table 
# 			where events are not null or none, along with the count of occurrences for each combination. from services_weekly;
#			Order by count descending.

SELECT service, event,

COUNT(*) AS occurrence_count

FROM services_weekly

WHERE event IS NOT NULL

AND event <> 'none'

GROUP BY service, event

ORDER BY occurrence_count DESC;

![solutions](/images/11.4.PNG)

/*
============================================================================

WHERE vs HAVING

Ask yourself:

"Am I filtering rows
or filtering groups?"

✅ Use WHERE

When filtering individual rows.

Examples:

WHERE age > 60

WHERE service = 'ICU'

WHERE event IS NOT NULL

----------------------------

✅ Use HAVING

When filtering aggregated values.

Examples:

HAVING COUNT(*) > 100

HAVING SUM(sales) > 10000

HAVING AVG(score) >= 80

Rule:

No aggregate function?

↓

Use WHERE.

Aggregate function?

↓

Use HAVING.

=======================================================================================

GROUP BY

↓

Creates buckets.

COUNT(*)

↓

Counts how many rows are inside each bucket.

Think:

GROUP BY = Make Buckets
COUNT(*) = Count the Balls in Each Bucket */

