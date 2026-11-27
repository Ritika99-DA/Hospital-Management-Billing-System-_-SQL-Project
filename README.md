# Hospital-Management-Billing-System-_-SQL-Project
Basic to Advanced SQL concepts covered

CREATE DATABASE hospital_management;
USE hospital_management;

-- Creation of Tables:

CREATE TABLE departments (
						  department_id INT PRIMARY KEY,
                          department_name VARCHAR(50) NOT NULL UNIQUE,
                          location VARCHAR(50)
);

CREATE TABLE doctors (
						  doctor_id INT PRIMARY KEY,
                          doctor_name VARCHAR(100) NOT NULL,
                          specialization VARCHAR(100),
                          salary DECIMAL(10,2),
                          department_id INT,
                          FOREIGN KEY (department_id) REFERENCES departments(department_id)
					 );
                     
CREATE TABLE patients (
						  patient_id INT PRIMARY KEY,
                          patient_name VARCHAR(100) NOT NULL,
                          gender VARCHAR(10),
                          date_of_birth DATE,
                          phone VARCHAR(15) UNIQUE,
                          city VARCHAR(50)
					 );	
                     
CREATE TABLE appointments (
						  appointment_id INT PRIMARY KEY,
                          patient_id INT,
                          FOREIGN KEY(patient_id) REFERENCES patients(patient_id),
                          doctor_id INT, 
                          FOREIGN KEY(doctor_id) REFERENCES doctors(doctor_id),
                          date_of_birth DATE,
                          appointment_date DATE,
                          appointment_time TIME,
                          status_ VARCHAR(20)
					 );	

CREATE TABLE rooms (
						  room_id INT PRIMARY KEY,
                          room_number VARCHAR(10) UNIQUE,
                          room_type VARCHAR(30),
                          daily_charge DECIMAL(10,2),
                          availability VARCHAR(20) 
					 );	
                     
CREATE TABLE admissions (
						  admission_id INT PRIMARY KEY,
						  patient_id INT,
                          FOREIGN KEY(patient_id) REFERENCES patients(patient_id),
                          room_id INT, 
                          FOREIGN KEY(room_id) REFERENCES rooms(room_id),
                          admission_date DATE,
                          discharge_date DATE 
						);
	
CREATE TABLE bills  (
			              bill_id INT PRIMARY KEY,
						  patient_id INT,
                          FOREIGN KEY(patient_id) REFERENCES patients(patient_id),
                          admission_id INT, 
                          FOREIGN KEY(admission_id) REFERENCES admissions(admission_id),
                          bill_date DATE,
                          consultation_charge DECIMAL(10,2),
                          medicine_charge DECIMAL(10,2),
                          room_charge DECIMAL(10,2),
						  other_charge DECIMAL(10,2),
                          payment_status VARCHAR(20)
					);
    
-- Insert Data:

INSERT INTO departments (department_id, department_name, location)
VALUES
(1, 'Cardiology', 'Building A - Floor 1'),
(2, 'Neurology', 'Building A - Floor 2'),
(3, 'Orthopedics', 'Building B - Floor 1'),
(4, 'Pediatrics', 'Building B - Floor 2'),
(5, 'General Medicine', 'Building C - Floor 1'); 

INSERT INTO doctors (doctor_id, doctor_name, specialization, salary, department_id)
VALUES
(101, 'Dr. Aarav Sharma', 'Cardiologist', 120000.00, 1),
(102, 'Dr. Meera Joshi', 'Interventional Cardiologist', 135000.00, 1),
(103, 'Dr. Rohan Deshmukh', 'Neurologist', 115000.00, 2),
(104, 'Dr. Priya Kulkarni', 'Neurosurgeon', 145000.00, 2),
(105, 'Dr. Aditya Patil', 'Orthopedic Surgeon', 125000.00, 3),
(106, 'Dr. Sneha Rao', 'Joint Replacement Specialist', 130000.00, 3),
(107, 'Dr. Kunal Mehta', 'Pediatrician', 95000.00, 4),
(108, 'Dr. Ananya Nair', 'Child Specialist', 100000.00, 4),
(109, 'Dr. Vikram Singh', 'General Physician', 85000.00, 5),
(110, 'Dr. Isha Gupta', 'Internal Medicine', 90000.00, 5);

INSERT INTO patients (patient_id, patient_name, gender, date_of_birth, phone, city)
VALUES
(201, 'Amit Verma', 'Male', '1985-04-12', '9000000001', 'Mumbai'),
(202, 'Neha Kapoor', 'Female', '1992-08-25', '9000000002', 'Pune'),
(203, 'Rahul Patil', 'Male', '1978-11-03', '9000000003', 'Nashik'),
(204, 'Sneha Desai', 'Female', '2001-02-17', '9000000004', 'Thane'),
(205, 'Arjun Malhotra', 'Male', '1995-06-09', '9000000005', 'Panvel'),
(206, 'Priyanka Shah', 'Female', '1988-12-21', '9000000006', 'Nagpur'),
(207, 'Siddharth Rao', 'Male', '1969-09-14', '9000000007', 'Mumbai'),
(208, 'Kavya Nair', 'Female', '2015-03-30', '9000000008', 'Pune'),
(209, 'Manish Yadav', 'Male', '1990-07-18', '9000000009', 'Aurangabad'),
(210, 'Riya Chavan', 'Female', '2003-10-05', '9000000010', 'Raigad'),
(211, 'Vivek Joshi', 'Male', '1975-01-26', '9000000011', 'Kolhapur'),
(212, 'Pooja Mishra', 'Female', '1998-05-11', '9000000012', 'Mumbai'),
(213, 'Sameer Khan', 'Male', '1982-03-19', '9000000013', 'Navi Mumbai'),
(214, 'Aditi Pawar', 'Female', '1996-09-07', '9000000014', 'Satara'),
(215, 'Nikhil Soni', 'Male', '2000-12-29', '9000000015', 'Pune');

INSERT INTO appointments (appointment_id, patient_id, doctor_id, date_of_birth,
						  appointment_date, appointment_time, status_)
VALUES
(301, 201, 101, '1985-04-12', '2025-01-10', '09:00:00', 'Completed'),
(302, 202, 103, '1992-08-25', '2025-01-11', '10:30:00', 'Completed'),
(303, 203, 105, '1978-11-03', '2025-01-12', '11:00:00', 'Completed'),
(304, 204, 107, '2001-02-17', '2025-01-13', '12:00:00', 'Cancelled'),
(305, 205, 109, '1995-06-09', '2025-01-14', '09:30:00', 'Completed'),
(306, 201, 102, '1985-04-12', '2025-01-20', '10:00:00', 'Completed'),
(307, 206, 101, '1988-12-21', '2025-01-21', '11:30:00', 'Completed'),
(308, 207, 104, '1969-09-14', '2025-01-22', '14:00:00', 'Completed'),
(309, 208, 108, '2015-03-30', '2025-01-23', '15:00:00', 'Cancelled'),
(310, 209, 110, '1990-07-18', '2025-01-24', '16:00:00', 'Completed'),
(311, 210, 107, '2003-10-05', '2025-02-01', '09:00:00', 'Scheduled'),
(312, 202, 103, '1992-08-25', '2025-02-02', '10:00:00', 'Completed'),
(313, 211, 105, '1975-01-26', '2025-02-03', '11:00:00', 'Scheduled'),
(314, 212, 109, '1998-05-11', '2025-02-04', '12:30:00', 'Completed'),
(315, 213, 102, '1982-03-19', '2025-02-05', '13:00:00', 'Cancelled'),
(316, 205, 106, '1995-06-09', '2025-02-10', '14:30:00', 'Completed'),
(317, 206, 101, '1988-12-21', '2025-02-11', '15:00:00', 'Scheduled'),
(318, 207, 110, '1969-09-14', '2025-02-12', '16:00:00', 'Completed'),
(319, 210, 108, '2003-10-05', '2025-02-13', '10:30:00', 'Scheduled'),
(320, 213, 104, '1982-03-19', '2025-02-14', '11:30:00', 'Completed');

INSERT INTO rooms (room_id, room_number, room_type, daily_charge, availability)
VALUES
(401, 'A101', 'General Ward', 1500.00, 'Occupied'),
(402, 'A102', 'General Ward', 1500.00, 'Occupied'),
(403, 'A103', 'Private Room', 3500.00, 'Occupied'),
(404, 'B201', 'Semi-Private', 2500.00, 'Occupied'),
(405, 'B202', 'ICU', 6000.00, 'Occupied'),
(406, 'B203', 'General Ward', 1500.00, 'Available'),
(407, 'C301', 'Private Room', 3500.00, 'Available'),
(408, 'C302', 'Semi-Private', 2500.00, 'Available'),
(409, 'C303', 'ICU', 6000.00, 'Available'),
(410, 'D401', 'General Ward', 1500.00, 'Available');

INSERT INTO admissions (admission_id, patient_id, room_id, admission_date, discharge_date)
VALUES
(501, 201, 401, '2025-01-05', '2025-01-09'),
(502, 202, 402, '2025-01-08', '2025-01-12'),
(503, 203, 403, '2025-01-10', '2025-01-15'),
(504, 204, 404, '2025-01-12', '2025-01-14'),
(505, 205, 405, '2025-01-15', '2025-01-20'),
(506, 206, 401, '2025-02-01', '2025-02-04'),
(507, 207, 402, '2025-02-05', '2025-02-10'),
(508, 208, 403, '2025-02-08', '2025-02-11'),
(509, 209, 404, '2025-02-12', '2025-02-16'),
(510, 210, 405, '2025-02-15', '2025-02-18');

INSERT INTO bills(bill_id, patient_id, admission_id, bill_date,
				  consultation_charge, medicine_charge, room_charge,
				  other_charge, payment_status)
VALUES
(601, 201, 501, '2025-01-09', 1500.00, 2500.00, 6000.00, 500.00, 'Paid'),
(602, 201, 501, '2025-01-10', 500.00, 1000.00, 0.00, 200.00, 'Unpaid'),
(603, 202, 502, '2025-01-12', 1200.00, 1800.00, 6000.00, 300.00, 'Paid'),
(604, 203, 503, '2025-01-15', 2000.00, 3500.00, 17500.00, 1000.00, 'Unpaid'),
(605, 204, 504, '2025-01-14', 800.00, 1200.00, 5000.00, 250.00, 'Paid'),
(606, 205, 505, '2025-01-20', 2500.00, 5000.00, 30000.00, 1500.00, 'Unpaid'),
(607, 206, 506, '2025-02-04', 1500.00, 2200.00, 4500.00, 400.00, 'Paid'),
(608, 207, 507, '2025-02-10', 1800.00, 3000.00, 17500.00, 800.00, 'Paid'),
(609, 208, 508, '2025-02-11', 1000.00, 1500.00, 10500.00, 300.00, 'Unpaid'),
(610, 209, 509, '2025-02-16', 1300.00, 2700.00, 10000.00, 500.00, 'Paid'),
(611, 210, 510, '2025-02-18', 900.00, 1600.00, 4500.00, 200.00, 'Paid'),
(612, 202, 502, '2025-01-13', 600.00, 800.00, 0.00, 150.00, 'Unpaid');


-- Basic Queries:
-- Display all patients. 
SELECT * FROM patients;

-- Display all doctors. 
SELECT * FROM doctors;

-- Display patients from Mumbai. 
SELECT * 
FROM patients
WHERE city = "Mumbai";

-- Display doctors whose salary is greater than 80000. 
SELECT * 
FROM doctors
WHERE salary > 80000; 

-- Display patients whose city is Mumbai, Pune or Nashik. 
SELECT * 
FROM patients
WHERE city IN ("Mumbai","Pune","Nashik");

-- Display doctors whose specialization contains Cardio. 
SELECT * 
FROM doctors
WHERE specialization LIKE "%Cardio%";

-- Display patients born between two dates. 
SELECT * 
FROM patients
WHERE date_of_birth BETWEEN 1992-08-25 AND 2001-02-17; 

-- Display appointments scheduled on a particular date. 
SELECT * 
FROM appointments
WHERE appointment_date = "2025-01-14"; 

-- Display patients whose phone number is NULL. 
SELECT * 
FROM patients
WHERE phone IS NULL; 

-- Display patients whose phone number is NOT NULL. 
SELECT * 
FROM patients;

-- Display doctors in ascending order of salary. 
SELECT * 
FROM doctors
ORDER BY salary; 

-- Display the five highest-paid doctors. 
SELECT * 
FROM doctors
ORDER BY salary DESC
LIMIT 5;

-- Display unique cities of patients. 
SELECT DISTINCT(city)
FROM patients; 

-- Aggregate Queries 

-- Find total patients. 
SELECT COUNT(*) AS total_patients
FROM patients;

-- Find total doctors. 
SELECT COUNT(*) AS total_doctors
FROM doctors; 

-- Find average doctor salary. 
SELECT AVG(salary) AS average_doctors
FROM doctors; 

-- Find highest doctor salary. 
SELECT * 
FROM doctors
ORDER BY salary DESC
LIMIT 1;   

-- Find lowest doctor salary. 
SELECT * 
FROM doctors
ORDER BY salary 
LIMIT 1;
 
-- Find total salary paid to all doctors. 
SELECT SUM(salary) AS total_salary
FROM doctors;

-- Find patients in each city. 
SELECT city,COUNT(patient_name) AS patient_count
FROM patients
GROUP BY city;

-- Find doctors in each department. 
SELECT department_name,COUNT(doctor_id) AS doctors_count
FROM doctors dc
JOIN 
departments de ON dc.department_id = de.department_id
GROUP BY department_name;

-- Find average salary in each department. 
SELECT department_name,AVG(salary) AS avg_salary_by_dept
FROM departments de
LEFT JOIN 
doctors dc ON de.department_id = dc.department_id
GROUP BY department_name;

-- Find departments having more than two doctors. 
SELECT department_name, COUNT(doctor_id) AS doctor_count
FROM departments de
LEFT JOIN 
doctors dc ON de.department_id = dc.department_id
GROUP BY department_name
HAVING doctor_count > 2;

-- Find total bill amount for each patient.
SELECT patient_id, (consultation_charge + medicine_charge + room_charge + other_charge) AS total_bill
FROM bills; 

ALTER TABLE bills
ADD COLUMN total_bill DECIMAL(10,2);

SELECT * FROM bills;
SET SQL_SAFE_UPDATES = 0;

UPDATE bills
SET total_bill = consultation_charge + medicine_charge + room_charge + other_charge;

SELECT * FROM bills;
       
-- Find patients whose total bills exceed ₹50,000. 
SELECT patient_id, SUM(total_bill) AS s
FROM bills
GROUP BY patient_id
HAVING s > 50000; 

-- JOIN Queries 

-- Display doctor name and department name. 
SELECT dc.doctor_name, de.department_name
FROM doctors dc
INNER JOIN 
departments de ON dc.department_id = de.department_id; 

-- Display patient name and appointment date. 
SELECT patient_name, appointment_date
FROM patients p
INNER JOIN 
		  appointments a ON p.patient_id = a.patient_id; 

-- Display patient name, doctor name and appointment date. 
SELECT patient_name, doctor_name, appointment_date 
FROM appointments a
JOIN patients p 
	 ON  a.patient_id = p.patient_id
JOIN doctors dc 
	 ON a.doctor_id = dc.doctor_id;

-- Display doctor name, specialization and department name. 
SELECT dc.doctor_name, dc.specialization, de.department_name
FROM doctors dc
INNER JOIN 
departments de ON dc.department_id = de.department_id; 

-- Display patient name, room number and admission date. 
SELECT patient_name, room_number, admission_date
FROM admissions a
JOIN  patients p ON  a.patient_id = p.patient_id
JOIN  rooms r ON a.room_id = r.room_id;

-- Display patient name, doctor name, specialization and appointment status. 
SELECT p.patient_name, dc.doctor_name, dc.specialization, a.status_
FROM appointments a
INNER JOIN 
patients p ON a.patient_id = p.patient_id
INNER JOIN 
doctors dc ON a.doctor_id = dc.doctor_id
INNER JOIN
departments de ON  dc.department_id = de.department_id;

-- Display patient name and total bill information. 
SELECT patient_name, total_bill
FROM patients p
JOIN 
     bills b ON p.patient_id = b.patient_id;
			
-- Display all patients including those who have never booked an appointment. 
SELECT p.patient_id, p.patient_name, a.status_, a.appointment_id
FROM patients p
LEFT JOIN 
     appointments a  ON p.patient_id = a.patient_id; 
     
-- Display all departments including those with no doctors. 
SELECT de.department_name , dc.doctor_id
FROM departments de
LEFT JOIN 
doctors dc ON de.department_id = dc.department_id;  

-- UPDATE and DELETE 
SET SQL_SAFE_UPDATES = 0;

-- Increase all doctor salaries by 10%. 
UPDATE doctors 
SET salary = salary * 1.10;
SELECT * FROM doctors;

-- Increase Cardiology doctor salaries by 15%. 
UPDATE doctors 
SET salary = salary + 0.15*salary
WHERE specialization LIKE "%Cardio%";

SELECT * FROM doctors;

-- Change a patient's city. 
UPDATE patients 
SET city = "Pune"
WHERE patient_id = 201;
SELECT * FROM patients; 

-- Mark an appointment Completed. 
UPDATE appointments
SET status_ = "Completed"
WHERE appointment_id = 304;

-- Mark all past scheduled appointments Completed. 
UPDATE appointments
SET status_ = "Completed"
WHERE status_ = "Scheduled";
SELECT * FROM appointments; 

-- Update bill payment status. 
UPDATE bills 
SET payment_status = "Paid"
WHERE bill_id = 602;

-- Delete a cancelled appointment. 
DELETE FROM appointments
WHERE status_ = "Cancelled";
SELECT * FROM appointments; 

-- Delete a patient who has never had an appointment. 
DELETE FROM appointments
WHERE status_ = "NULL";
SELECT * FROM appointments;   
  
-- ALTER TABLE 
-- Add email to patients. 
SELECT * FROM patients; 
ALTER TABLE patients
ADD COLUMN email VARCHAR(40);

-- Add emergency_contact. 
ALTER TABLE patients
ADD COLUMN emergency_contact INT;

-- Modify specialization column size. 
SELECT * FROM doctors; 
ALTER TABLE doctors
MODIFY COLUMN specialization VARCHAR (70);
describe doctors;

-- Rename other_charge to additional_charge. 
SELECT * FROM bills; 
ALTER TABLE bills
RENAME COLUMN other_charge TO additional_charge;

-- Add a constraint ensuring room charges cannot be negative. 
describe rooms;
ALTER TABLE rooms
MODIFY COLUMN daily_charge DECIMAL(10,2) NOT NULL;

-- Remove an unnecessary column.   
ALTER TABLE patients
DROP emergency_contact;
SELECT * FROM patients;

-- Subqueries 
 
-- Find doctors earning more than average salary. 
SELECT doctor_name,salary
FROM doctors
WHERE salary > (SELECT avg(salary) AS avg_salary
				FROM doctors); 

-- Find the highest-paid doctor. 
SELECT doctor_name,salary
FROM doctors
WHERE salary = (SELECT salary
				FROM doctors
                ORDER BY salary DESC
                LIMIT 1);

-- Find patients with appointments with Cardiology doctors. 
SELECT a.patient_id, doctor_id
FROM appointments a
WHERE doctor_id IN   (SELECT doctor_id
					  FROM doctors d 
					  WHERE department_id = (SELECT department_id
											  FROM departments  
											  WHERE department_name = "Cardiology")
					 ); 

-- Find patients who never booked an appointment. 
SELECT patient_id 
FROM appointments
WHERE patient_id NOT IN (SELECT patient_id 
						FROM appointments);
                        
SELECT * FROM appointments; 

-- Find departments whose average salary exceeds the overall average. 

SELECT de.department_name, dc.department_id
FROM departments de
INNER JOIN 
	 doctors dc on de.department_id = dc.department_id
GROUP BY dc.department_id, de.department_name
HAVING AVG(dc.salary) > (SELECT avg(salary)
                         FROM doctors);  

-- Find patient with highest total bill. 
SELECT patient_id, total_bill
FROM bills
WHERE total_bill = ( SELECT max(total_bill)
					FROM bills);

-- Find doctors who never received an appointment.
SELECT dc.doctor_id
FROM doctors dc
WHERE doctor_id NOT IN (SELECT doctor_id
						FROM appointments);  

-- Find patients whose total bill exceeds the average patient bill. - doubt
SELECT patient_id, SUM(total_bill) 
FROM bills b
GROUP BY patient_id
HAVING SUM(total_bill)  > (SELECT(avg(b.total_bill)) AS AVG_BILL
						FROM bills); 
                     
SELECT * FROM bills; 


-- Views 

-- Create patient_appointment_details with patient name, doctor name, specialization, department, appointment date/time and status. 
CREATE OR REPLACE VIEW patient_appointment_details AS 

SELECT patient_name, doctor_name, specialization,department_name, appointment_date,status_
FROM appointments a
JOIN patients p 
	 ON  a.patient_id = p.patient_id
JOIN doctors dc 
	 ON a.doctor_id = dc.doctor_id
JOIN departments de
     ON dc.department_id = de.department_id;

-- Query the complete view. 
SELECT * FROM patient_appointment_details;

-- Query only completed appointments. 
SELECT * 
FROM patient_appointment_details
WHERE status_ = "Completed";

-- Query appointments for a particular doctor. 
SELECT * 
FROM patient_appointment_details
WHERE doctor_name = "Dr. Aarav Sharma"; 

-- Query appointments for a particular department. 
SELECT * 
FROM patient_appointment_details
WHERE department_name = "Cardiology"; 

-- Create patient_bill_summary with patient_id, patient_name, total_bill and payment_status. 

CREATE OR REPLACE VIEW patient_bill_summary AS  

SELECT p.patient_id, p.patient_name, b.total_bill, b.payment_status
FROM patients p
INNER JOIN 
		  bills b ON p.patient_id = b.patient_id;
          
-- Query the bill summary view. 
SELECT * 
FROM patient_bill_summary; 

-- Built-in Functions 

-- Display patient names in uppercase. 
SELECT upper(patient_name)
FROM patients;

-- Display patient names in lowercase. 
SELECT lower(patient_name)
FROM patients; 

-- Display name lengths. 
SELECT length(patient_name)
FROM patients; 

-- Display first three characters of names. 
SELECT left(patient_name,3)
FROM patients; 

-- Concatenate patient name and city.    
SELECT concat(patient_name, " ", city)
FROM patients;

-- Calculate patient ages. 
SELECT patient_name,
	   timestampdiff(year, date_of_birth, CURDATE()) AS age
FROM patients; 

-- Display current date. 
SELECT CURDATE();

-- Calculate days between admission and discharge.
SELECT a.appointment_id, a.patient_id,
       DATEDIFF(bill_date, appointment_date) AS total_days
FROM bills b
JOIN 
     appointments a ON b.patient_id = a.patient_id
WHERE b.bill_date > a.appointment_date;

-- Find patients admitted in the current year. 
SELECT p.patient_id, p.patient_name, a.appointment_date,
       year(CURDATE()) AS appointment_year
FROM patients p 
JOIN appointments a ON p.patient_id = a.patient_id
WHERE YEAR(a.appointment_date) = YEAR(CURDATE()); 

-- Extract year and month from appointment dates. 
SELECT appointment_date,
       YEAR(appointment_date),
       MONTHNAME(appointment_date)
FROM appointments; 

-- Round doctor salaries to the nearest thousand. 
SELECT doctor_name, round(salary,-3) as rounded_salary
FROM doctors;

-- Calculate 10% tax on bills. 
SELECT total_bill,
	   (0.10*total_bill) AS tax
FROM bills; 

-- Calculate final bill after 18% GST. 
SELECT total_bill,
	   (total_bill + 0.18*total_bill ) AS including_gst
FROM bills;

-- Stored Functions   

-- Create calculate_age(date_of_birth) returning current age. 
DELIMITER $$

CREATE FUNCTION calculate_age(
	date_of_birth DATE
)
RETURNS INT
DETERMINISTIC 
NO SQL
BEGIN 
	DECLARE age INT;

    SET age = TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE());

	RETURN age;
END$$

DELIMITER ;

SELECT
    patient_id,
    date_of_birth,
    calculate_age(date_of_birth) AS age
FROM patients;


-- Create calculate_bill_total(consultation_charge, medicine_charge, room_charge, additional_charge) returning total bill. 
DELIMITER $$

CREATE FUNCTION calculate_bill_total(
consultation_charge DECIMAL(10,2),
medicine_charge DECIMAL(10,2),
room_charge DECIMAL(10,2),
additional_charge DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)

DETERMINISTIC 
NO SQL

BEGIN 
	DECLARE total_bill DECIMAL(10,2);
    
    SET total_bill = consultation_charge + medicine_charge + room_charge + additional_charge;
    
    RETURN total_bill;
END $$

DELIMITER ;
SELECT calculate_bill_total(
        consultation_charge,
        medicine_charge,
        room_charge,
        other_charge
    ) AS calculated_total
FROM bills; 

-- Use both functions in SELECT queries. 
SELECT calculate_bill_total(
        consultation_charge,
        medicine_charge,
        room_charge,
        other_charge
    ) AS calculated_total
FROM bills; 

SELECT
    patient_id,
    date_of_birth,
    calculate_age(date_of_birth) AS age
FROM patients;

-- Stored Procedures 

-- Create get_patient_details(patient_id) displaying name, gender, date of birth, phone and city. 
DELIMITER //

CREATE PROCEDURE patient_details(
     IN p_patient_id INT 
     )
BEGIN 
	  SELECT  gender, date_of_birth, phone, city 
      FROM patients 
      WHERE p_patient_id = patient_id;
END //

DELIMITER ;

CALL patient_details(202); 

-- Create update_doctor_salary(doctor_id, percentage) to update salary. Example: CALL update_doctor_salary(101, 10).                
DELIMITER //

CREATE PROCEDURE update_doctor_salary(
 IN d_doctor_id INT,
 IN d_percentage DECIMAL(10,2)
 )
  
BEGIN 
    UPDATE doctors
	SET salary = salary + (salary * d_percentage/100)
	WHERE doctor_id = d_doctor_id;
END // 

DELIMITER ;

CALL update_doctor_salary(101, 10);

SELECT * FROM doctors; 
 
-- Procedure with IF/ELSE   

-- Create check_bill_status(bill_id). If Paid, display 'Bill has been paid'; otherwise display 'Payment is pending'. 

DELIMITER //

CREATE PROCEDURE check_bill_status(
IN p_bill_id INT 
)
BEGIN
    DECLARE v_payment_status VARCHAR(20);

    SELECT payment_status
    INTO v_payment_status
    FROM bills
    WHERE bill_id = p_bill_id;

    IF v_payment_status = 'Paid' THEN
        SELECT 'Bill has been paid' AS message;
    ELSE
        SELECT 'Payment is pending' AS message;
    END IF;
END //
)
DELIMITER ;

CALL check_bill_status(601);

-- Procedure with OUT Parameter 

-- Create get_patient_bill(patient_id, OUT total_amount) to calculate total bill. 

-- Call: CALL get_patient_bill(101, @total); SELECT @total; 

DELIMITER //

CREATE PROCEDURE get_patient_bill(
    OUT total_amount DECIMAL(10,2)
)
BEGIN
    SET total_amount = (
        SELECT SUM(total_bill)
        FROM bills
    );
END //

DELIMITER ; 

SET @total = 0;

CALL get_patient_bill(@total);

SELECT @total AS total_amount;

-- Exception Handling   

-- Create add_appointment(appointment_id, patient_id, doctor_id, appointment_date, appointment_time). 

-- Handle SQL exceptions using DECLARE EXIT HANDLER FOR SQLEXCEPTION. 

-- If insertion fails, display 'Appointment could not be created.'     

-- Exception Handling

DELIMITER //

CREATE PROCEDURE add_appointment(
    IN p_appointment_id INT,
    IN p_patient_id INT,
    IN p_doctor_id INT,
    IN p_appointment_date DATE,
    IN p_appointment_time TIME
)
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION
    BEGIN
        SELECT 'Appointment could not be created.' AS message;
    END;

    INSERT INTO appointments(
        appointment_id,
        patient_id,
        doctor_id,
        appointment_date,
        appointment_time
    )
    VALUES (
        p_appointment_id,
        p_patient_id,
        p_doctor_id,
        p_appointment_date,
        p_appointment_time
    );

END //

DELIMITER ;

CALL add_appointment(
    501,
    201,
    101,
    '2026-12-01',
    '10:30:00'
);

CALL add_appointment(
    501,
    201,
    101,
    '2026-12-01',
    '10:30:00'
);

-- SIGNAL 

-- Modify the appointment procedure so a past appointment date generates 'Appointment date cannot be in the past.' using SIGNAL SQLSTATE '45000'. 

-- Prevent an appointment if the patient does not exist. 

DELIMITER //

CREATE PROCEDURE add_appointment1(
    IN p_appointment_id INT,
    IN p_patient_id INT,
    IN p_doctor_id INT,
    IN p_appointment_date DATE,
    IN p_appointment_time TIME

)
BEGIN

	IF p_appointment_date < CURDATE()  THEN 
		
        SIGNAL SQLSTATE  '45000'
        SET MESSAGE_TEXT = 
			'Appointment date cannot be in the past'; 
    END IF;

     IF NOT EXISTS (
        SELECT 1
        FROM patients
        WHERE patient_id = p_patient_id
    ) THEN

        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Patient does not exist.';

    END IF;
    
    INSERT INTO appointments(
        appointment_id,
        patient_id,
        doctor_id,
        appointment_date,
        appointment_time
    )
    VALUES (
        p_appointment_id,
        p_patient_id,
        p_doctor_id,
        p_appointment_date,
        p_appointment_time
    );

END //

DELIMITER ;
DROP PROCEDURE add_appointment1;
CALL add_appointment1(501, 201, 101, '2025-01-01', '10:30:00');

CALL add_appointment(502, 309, 101, '2026-12-01', '10:30:00');

-- Trigger — Appointment Audit 

-- Create appointment_audit with audit_id, appointment_id, patient_id, doctor_id, old_status, new_status and changed_on. 
-- -- Create a trigger that records appointment status changes. 
 
CREATE TABLE appointment_audit (
                audit_id INT AUTO_INCREMENT PRIMARY KEY, 
                appointment_id INT, 
                patient_id INT,
                doctor_id INT, 
                old_status VARCHAR(40),
                new_status VARCHAR(40),
				changed_on datetime default current_timestamp
                );
                
CREATE TABLE appointment_status_log(
    appointment_id int primary key auto_increment,
    log text
);

 DELIMITER //
 
 CREATE TRIGGER after_appointment_update
 AFTER UPDATE ON appointments
 FOR EACH ROW
 BEGIN 
	INSERT INTO appointment_audit(appointment_id, patient_id, doctor_id, old_status, new_status)
		       VALUES ( OLD.appointment_id, OLD.patient_id, OLD.doctor_id, OLD.status_, NEW.status_
					  );
    
    INSERT INTO appointment_status_log(log)
			VALUES ( CONCAT('Appointment ', OLD.appointment_id, ' status changed from ', OLD.status_, ' to ', NEW.status_ )
				   );
 END//
DELIMITER ;

SELECT * FROM appointments;

UPDATE appointments
SET status_ = 'Completed'
WHERE appointment_id = 302;

SELECT * FROM appointment_audit;
SELECT * FROM appointment_status_log;

-- Trigger — Room Availability 
-- When a patient is admitted, automatically change room availability to Occupied. 

-- When a patient is discharged, automatically change room availability to Available.

SELECT * FROM admissions;
SELECT * FROM rooms;

#After insert trigger used because initially patients are admitted in the rooms after they come in. 

DELIMITER //

CREATE TRIGGER after_admission_insert
AFTER INSERT ON admissions
FOR EACH ROW
BEGIN

    UPDATE rooms
    SET availability = 'Occupied'
    WHERE room_id = NEW.room_id;

END //

DELIMITER ;

#after update trigger will be used as the status of rooms is updated to available once patients leave. 
DELIMITER //

CREATE TRIGGER after_admission_update
AFTER UPDATE ON admissions
FOR EACH ROW
BEGIN

    IF OLD.discharge_date IS NULL
       AND NEW.discharge_date IS NOT NULL THEN

        UPDATE rooms
        SET availability = 'Available'
        WHERE room_id = NEW.room_id;

    END IF;

END //

DELIMITER ;

INSERT INTO admissions (
    admission_id,
    patient_id,
    room_id,
    admission_date,
    discharge_date
)
VALUES (703, 201, 405, CURDATE(), NULL);

SELECT * FROM rooms;

UPDATE admissions
SET discharge_date = CURDATE()
WHERE admission_id = 703;

SELECT * FROM rooms;
 
-- Trigger — Bill Validation 

-- Prevent bill insertion if any charge is negative. 

-- Generate an appropriate error using SIGNAL SQLSTATE '45000'. 
SELECT * FROM bills;

DELIMITER //

CREATE TRIGGER before_bills_insert
BEFORE INSERT ON bills
FOR EACH ROW

BEGIN
	IF NEW.consultation_charge < 0 OR
       NEW.medicine_charge < 0 OR
       NEW.room_charge < 0 OR
       NEW.other_charge <0 
       
       THEN 
		
        SIGNAL SQLSTATE  '45000'
        SET MESSAGE_TEXT = 
			'Any Bill charges cannot be negative'; 
    END IF;
END //

DELIMITER ;

INSERT INTO bills (bill_id, patient_id, consultation_charge, medicine_charge, room_charge, other_charge)
VALUES (604, 203, -800, 1000, -9000, 500);

-- Trigger — Automatic Bill Date 

-- Automatically set bill_date = CURDATE(), when a bill is inserted without a bill date. 

SELECT * FROM bills;
DELIMITER //

CREATE TRIGGER INSERT_before_bill_date
BEFORE INSERT ON bills
FOR EACH ROW

BEGIN
	IF NEW.bill_date = NULL
       THEN 
	   SET NEW.bill_date = CURDATE();
    END IF;
END //

DELIMITER ;

INSERT INTO bills (bill_id, patient_id, consultation_charge, medicine_charge, room_charge, other_charge)
VALUES (699, 201, 500, 1000, 2000, 500);

SELECT*FROM bills;

-- Transactions 

-- For patient discharge: update admission discharge date, make room available, calculate room charge, update bill and mark bill pending. 

-- Perform all operations inside a transaction using START TRANSACTION and COMMIT. 
 SELECT * FROM rooms; 

SELECT * FROM admissions; 

SELECT * FROM bills; 

 START TRANSACTION; 
 
 UPDATE admissions
 SET discharge_date = CURDATE()
 WHERE admission_id = 703;
 
 UPDATE rooms
 SET availability = "Available"
 WHERE room_id = (  SELECT room_id
					FROM admissions
					WHERE admission_id = 703);
                    
UPDATE bills b
JOIN admissions a ON b.admission_id = a.admission_id
JOIN rooms r ON a.room_id = r.room_id
SET
    b.room_charge = DATEDIFF(a.discharge_date, a.admission_date) * r.daily_charge,

    b.total_bill = b.consultation_charge
                 + b.medicine_charge
                 + b.room_charge
                 + b.other_charge,

    b.payment_status = 'Pending'

WHERE a.admission_id = 703;

COMMIT;


-- SAVEPOINT 

-- Create a transaction for patient discharge, room update and bill update. 

-- Create a savepoint after the room update. 

-- Perform an intentionally incorrect operation. 

-- Use ROLLBACK TO SAVEPOINT and then COMMIT. 

-- Verify which changes remain. 
START TRANSACTION; 
 
 UPDATE admissions
 SET discharge_date = CURDATE()
 WHERE admission_id = 502;
 
 UPDATE rooms
 SET availability = "Available"
 WHERE room_id = (  SELECT room_id
					FROM admissions
					WHERE admission_id = 502);
SAVEPOINT after_room_update;

UPDATE bills
SET total_bill = -8000
WHERE admission_id = 502;

ROLLBACK TO SAVEPOINT after_room_update;

SELECT * 
FROM bills 
WHERE admission_id = 502;
                    
UPDATE bills
SET payment_status = 'Completedmmmm'
WHERE admission_id = 502;

COMMIT;
 
SELECT * 
FROM bills 
WHERE admission_id = 502;
  
-- ROLLBACK 

-- Update patient information, bill and admission inside a transaction. 
-- Use ROLLBACK. 
-- Verify that none of the changes remain.   

SELECT * FROM patients;
SELECT * FROM admissions; 
SELECT * FROM bills;

START TRANSACTION;

UPDATE patients
SET gender = "Female"
WHERE patient_id = 205;

UPDATE admissions
SET admission_date = "2025-02-11"
WHERE patient_id = 205;

UPDATE bills
SET payment_status = "Paid"
WHERE patient_id = 205;

ROLLBACK; 

SELECT * FROM patients
WHERE patient_id = 205;

SELECT * FROM admissions
WHERE patient_id = 205;

SELECT * FROM bills
WHERE patient_id = 205;

-- METADATA:
SHOW TABLES;
DESCRIBE patients;
DESCRIBE doctors;
SHOW CREATE TABLE appointments;
SHOW INDEX FROM patients;
SHOW TRIGGERS;
SHOW PROCEDURE STATUS;
SHOW FUNCTION STATUS;
 
-- Query Optimization
-- Create an appropriate index and run EXPLAIN again. Compare the execution plan before and after the index and identify columns that can benefit from indexing.

-- Before index execution:

EXPLAIN
SELECT p.patient_name, d.doctor_name, a.appointment_date 
FROM patients p 
JOIN appointments a ON p.patient_id = a.patient_id 
JOIN doctors d ON a.doctor_id = d.doctor_id 
WHERE p.city = 'Mumbai';

CREATE INDEX city_name
ON patients(city);

EXPLAIN
SELECT p.patient_name, d.doctor_name, a.appointment_date 
FROM patients p 
JOIN appointments a ON p.patient_id = a.patient_id 
JOIN doctors d ON a.doctor_id = d.doctor_id 
WHERE p.city = 'Mumbai';

-- Observation post using index: Before creating the index, MySQL followed its usual process to find patients from Mumbai. After creating an index on patients.city, it became easier for MySQL to find the matching patients. We can also create indexes on appointments.patient_id and appointments.doctor_id to make joining the tables faster, as these columns are used to connect the tables. 

SHOW INDEX FROM patients;

  -- Final Integrated Challenge:
  
  DELIMITER // 

  CREATE PROCEDURE complete_patient_discharge(IN p_patient_id INT)
  
  BEGIN 
  
        DECLARE EXIT HANDLER FOR SQLEXCEPTION
		BEGIN
			ROLLBACK TO SAVEPOINT discharge_savepoint;
			ROLLBACK;

        SELECT 'Patient discharge failed.' AS message;
        SELECT 'All changes have been rolled back.' AS message;
    END;
        
        START TRANSACTION;
        
        SAVEPOINT discharge_savepoint;
        
		IF NOT EXISTS (
			SELECT *
			FROM admissions
			WHERE patient_id = p_patient_id
				AND discharge_date IS NULL)
	   THEN
			SIGNAL SQLSTATE '45000'
			SET MESSAGE_TEXT = 'Patient has no active admission.';
		END IF;
        
		IF NOT EXISTS (
			SELECT *
			FROM admissions a
			JOIN rooms r ON a.room_id = r.room_id
			WHERE a.patient_id = p_patient_id
			  AND a.discharge_date IS NULL) 
		THEN
			SIGNAL SQLSTATE '45000'
			SET MESSAGE_TEXT = 'Assigned room cannot be found.';
		END IF;
				
        SELECT * ,
			   DATEDIFF(CURDATE(), a.admission_date) AS days_stayed,
               (r.dailycharge * DATEDIFF(CURDATE(), a.admission_date)) AS room_charge
        FROM admissions a 
        JOIN rooms r ON a.room_id = r.room_id 
        WHERE a.patient_id = p_patient_id
          AND a.discharge_date IS NULL;
          
		UPDATE bills b 
			JOIN admissions a ON b.admission_id = a.admission_id
			JOIN rooms r ON a.room_id = r.room_id
        SET b.room_charge = r.dailycharge * (DATEDIFF(CURDATE(), a.admission_date)),
			b.payment_status = 'Pending' 
            
		WHERE a.patient_id = p_patient_id
          AND a.discharge_date IS NULL;
		
        UPDATE rooms
		SET availability = 'Available'
		WHERE room_id = (
			SELECT room_id
			FROM admissions
			WHERE patient_id = p_patient_id
			  AND discharge_date IS NULL
			LIMIT 1);
            
	   UPDATE admissions
	   SET discharge_date = CURDATE()
	   WHERE patient_id = p_patient_id
				AND discharge_date IS NULL;
       
       COMMIT;
       
  END // 
  
  DELIMITER ; 
  
  CALL complete_patient_discharge(204); 
