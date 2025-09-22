# JohnClinicBooking_system
A Clinic Booking Management System Database, that contains only Create database, create tables as the deliverables 



Here’s a README.md that explains your SQL schema, focusing on the syntax and structure rather than rewriting the code itself:


---

John Clinic Booking System – Database Schema

This project defines the database schema for a clinic appointment and treatment booking system using SQL. The schema demonstrates different relationship types (1:1, 1:N, M:N) and proper database design principles.


---

📌 Database Creation

CREATE DATABASE JohnClinicBooking_System;
USE JohnClinicBooking_System;

CREATE DATABASE → Creates a new database named JohnClinicBooking_System.

USE → Selects the database so that all subsequent SQL statements run inside it.



---

📌 Table Definitions

1. Patients Table

CREATE TABLE Patients (
    patient_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(70) NOT NULL,
    last_name VARCHAR(70) NOT NULL,
    date_of_birth DATE,
    phone VARCHAR(70),
    email VARCHAR(70) UNIQUE
);

patient_id INT AUTO_INCREMENT PRIMARY KEY → Creates a unique identifier for each patient, automatically increasing with each entry.

VARCHAR(70) → Defines text columns with a maximum length of 70 characters.

NOT NULL → Ensures the field cannot be left empty.

UNIQUE → Prevents duplicate values (e.g., no two patients with the same email).

DATE → Used for date_of_birth.



---

2. Doctors Table

CREATE TABLE Doctors (
    doctor_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(60) NOT NULL,
    last_name VARCHAR(60) NOT NULL,
    specialty VARCHAR(200)
);

doctor_id → Works the same way as patient_id.

specialty → Defines the doctor’s field (e.g., cardiology, pediatrics).



---

3. Appointments Table

CREATE TABLE Appointments (
    appointment_id INT AUTO_INCREMENT PRIMARY KEY,
    patient_id INT NOT NULL,
    doctor_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    reason TEXT,
    FOREIGN KEY (patient_id) REFERENCES Patients(patient_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);

appointment_id → Unique ID for each appointment.

DATETIME → Stores both date and time of appointment.

TEXT → Used for longer, variable-length strings (reason for visit).

FOREIGN KEY → Links the table to Patients and Doctors, enforcing referential integrity.

One Patient → Many Appointments (1:N).

One Doctor → Many Appointments (1:N).




---

4. Treatments Table

CREATE TABLE Treatments (
    treatment_id INT AUTO_INCREMENT PRIMARY KEY,
    treatment_name VARCHAR(200) NOT NULL,
    description TEXT
);

Defines available treatments (e.g., physical therapy, surgery).

Stored independently so multiple doctors can offer the same treatment.



---

5. Doctor_Treatments (Many-to-Many Relationship)

CREATE TABLE Doctor_Treatments (
    doctor_id INT NOT NULL,
    treatment_id INT NOT NULL,
    PRIMARY KEY (doctor_id, treatment_id),
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id),
    FOREIGN KEY (treatment_id) REFERENCES Treatments(treatment_id)
);

Composite Primary Key (doctor_id, treatment_id) → Prevents duplicate doctor-treatment pairs.

Models a many-to-many (M:N) relationship:

One doctor can offer multiple treatments.

One treatment can be offered by multiple doctors.




---

6. Doctor_Offices (One-to-One Relationship)

CREATE TABLE Doctor_Offices (
    doctor_id INT NOT NULL PRIMARY KEY,
    office_location VARCHAR(250) NOT NULL,
    FOREIGN KEY (doctor_id) REFERENCES Doctors(doctor_id)
);

Primary Key = doctor_id → Ensures one office is linked to exactly one doctor.

Represents a one-to-one (1:1) relationship:

Each doctor has only one office.

Each office belongs to only one doctor.




---

📌 Relationship Summary

Patients → Appointments: One-to-Many

Doctors → Appointments: One-to-Many

Doctors ↔ Treatments: Many-to-Many (via Doctor_Treatments)

Doctors → Offices: One-to-One



---

📌 Key SQL Concepts in Use

PRIMARY KEY → Unique identifier for each record.

AUTO_INCREMENT → Automatically generates sequential IDs.

FOREIGN KEY → Ensures data integrity between related tables.

NOT NULL → Prevents missing critical values.

UNIQUE → Avoids duplicate data in certain fields (like email).

VARCHAR vs TEXT vs DATE/DATETIME → Different data types for strings, large text, and date/time.



---

✅ This schema is structured to handle patient management, doctor details, scheduling, and treatment offerings in a normalized, relational way.


---

Do you want me to also add an ER diagram illustration (visual relationships) in the README to make it easier to understand, or keep it strictly text-based?

