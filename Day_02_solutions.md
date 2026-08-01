### Practice Questions:

# 1.Find all patients who are older than 60 years.

select * from patients where age > 60;

![solution](images/day_01_1st.PNG)


# 2. Retrieve all staff members who work in the 'Emergency' service.

select * from staff
where service like "%emer%";


# 3. List all weeks where more than 100 patients requested admission in any service.

select distinct(week) from services_weekly
where patients_request > 100;


### Daily Challenge:

# Find all patients admitted to 'Surgery' service with a satisfaction score below 70, 
# showing their patient_id, name, age, and satisfaction score.

select patient_id,name,age,satisfaction from patients
where service = "surgery" and satisfaction < 70;
