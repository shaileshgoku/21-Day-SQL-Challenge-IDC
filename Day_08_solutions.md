# 1. Convert all patient names to uppercase.

select upper(name) as patient_name from patients;

![solutions](/images/8.1.PNG)


# 2. Find the length of each staff member's name.

select staff_name,length(staff_name) as staff_name_length from staff;

![solutions](/images/8.2.PNG)


# 3. Concatenate staff_id and staff_name with a hyphen separator.

select concat(staff_id,"-",staff_name) as combined_id_name from staff;

![solutions](/images/8.3.PNG)


# Question: Create a patient summary that shows patient_id, full name in uppercase, service in lowercase, 
#			age category (if age >= 65 then 'Senior', if age >= 18 then 'Adult', else 'Minor'), 
#           and name length. Only show patients whose name length is greater than 10 characters.

SELECT patient_id,

UPPER(name) AS patient_name,

LOWER(service) AS service,

age,

CASE

WHEN age >= 65 THEN 'Senior'

WHEN age >= 18 THEN 'Adult'

ELSE 'Minor'

END AS age_category,

LENGTH(name) AS name_length

FROM patients

WHERE LENGTH(name) > 10;

========================================================================================================

WHERE filters rows.

If the condition uses columns from the current row,
write it directly.

✅ Correct

WHERE LENGTH(name) > 10

❌ Wrong

WHERE (
    SELECT LENGTH(name) > 10
)

Use a subquery only when you need data
from another query or another result set.

Rule:

If the value exists in the current row,
don't use a subquery.


![solutions](/images/8.4.PNG)

