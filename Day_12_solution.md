
# 1. Find all weeks in services_weekly where no special event occurred.

select distinct week from services_weekly

where event = 'none';

![solutions](/images/12.1.PNG)

# 2. Count how many records have null or empty event values.

SELECT COUNT(*) AS invalid_event_count

FROM services_weekly

WHERE event IS NULL

OR event = '';

![solutions](/images/12.2.PNG)

# 3. List all services that had at least one week with a special event.

SELECT DISTINCT service

FROM services_weekly

WHERE event IS NOT NULL

AND event <> 'none';

![solutions](/images/12.3.PNG)


# Question: Analyze the event impact by comparing weeks with events vs weeks without events. 
#           Show: event status ('With Event' or 'No Event'), count of weeks, average patient satisfaction, 
#           and average staff morale. Order by average patient satisfaction descending.

WITH weekly_status AS (

SELECT

week,

MAX(

CASE

WHEN event IS NOT NULL

AND event <> 'none'

THEN 1
                
ELSE 0
            
END
        
) AS has_event
    
FROM services_weekly
    
GROUP BY week

)

SELECT
    
CASE
        
WHEN ws.has_event = 1 THEN 'With Event'
        
ELSE 'No Event'
    
END AS event_status,
    
COUNT(DISTINCT sw.week) AS week_count,
    
ROUND(AVG(sw.patient_satisfaction), 2) AS avg_patient_satisfaction,
    
ROUND(AVG(sw.staff_morale), 2) AS avg_staff_morale

FROM services_weekly AS sw

JOIN weekly_status AS ws
    
    ON sw.week = ws.week

GROUP BY ws.has_event

ORDER BY avg_patient_satisfaction DESC;

![solutions](/images/12.4.PNG)


WITH weekly_status AS (
SELECT
week,
MAX(
CASE
WHEN event IS NOT NULL
AND event <> 'none'
THEN 1
ELSE 0
END
) AS has_event
FROM services_weekly
GROUP BY week
)
SELECT
CASE
WHEN ws.has_event = 1 THEN 'With Event'
ELSE 'No Event'
END AS event_status,
COUNT(DISTINCT sw.week) AS week_count,
ROUND(AVG(sw.patient_satisfaction), 2) AS avg_patient_satisfaction,
ROUND(AVG(sw.staff_morale), 2) AS avg_staff_morale
FROM services_weekly AS sw
JOIN weekly_status AS ws
ON sw.week = ws.week
GROUP BY ws.has_event
ORDER BY avg_patient_satisfaction DESC;
