# Healthcare-SQL-Analysis

This project focuses on cleaning and analyzing a healthcare dataset using PostgreSQL. Due to data integrity issues, financial analysis was excluded. The project demonstrates SQL data cleaning, integrity checks, and general insights.

---

## Project Repository Includes

This repository contains the following files and directories:

### 1. **Raw Data** (`Raw Data/`)
- Contains the original dataset before cleaning and processing.
- The dataset is fictional and sourced from Kaggle. You can access it [here](https://www.kaggle.com/datasets/anouskaabhisikta/healthcare-management-system).
- **Instructions:**
  - Click on any file to preview or download.
  - Open in Microsoft Excel or a compatible tool.

### 2. **Cleaned Data** (`Cleaned Data/`)
- Contains the fully cleaned dataset after integrity checks and reordering.
- **Instructions:**
  - Click on any file to preview or download.
  - Open in Microsoft Excel or a compatible tool.

### 3. **Data Cleaning Queries** (`Data Cleaning Queries/`)
- SQL scripts used to clean the dataset, remove duplicates, and correct inconsistencies.
- **Instructions:**
  - Screenshots of **SQL queries** used to clean the dataset.
   - Queries address duplicate records, renumbering IDs, and fixing data inconsistencies.

### 4. **Data Integrity Queries** (`Data Integrity Queries/`)
- SQL queries used to check for missing values, duplicate IDs, and orphaned records.
- **Instructions:**
  - Screenshots of **SQL queries** used to check for missing, inconsistent, or orphaned records.
   - This step ensured all primary and foreign keys aligned correctly.

### 5. **Data Validation Queries** (`Data Validation Queries/`)
- SQL queries used to validate the correctness of links between tables.
- **Instructions:**
  - Screenshots of **SQL queries** used to verify the correctness of the cleaned dataset.
   - Focuses on confirming patient-doctor relationships, appointment tracking, and billing consistency.

### 6. **Data Analysis Queries** (`Data Analysis Queries/`)
- SQL queries used for insights on patient trends, doctor workloads, and appointment distributions.
- **Instructions:**
  - Screenshots of **SQL queries** used for exploratory data analysis.
   - Includes queries on appointment trends, doctor workloads, and procedural insights.

---

## **About the Dataset**

The dataset consists of five key tables:

### **1. Patient Table (`patient`)**
- **Columns:**
  - `patient_id` (Primary Key) – Unique identifier for each patient.
  - `first_name` – Patient's first name.
  - `last_name` – Patient's last name.
  - `email` – Patient’s contact email.

### **2. Doctor Table (`doctor`)**
- **Columns:**
  - `doctor_id` (Primary Key) – Unique identifier for each doctor.
  - `doctor_name` – Full name of the doctor.
  - `specialization` – Medical field of expertise.
  - `doctor_contact` – Contact details for the doctor.

### **3. Appointment Table (`appointment`)**
- **Columns:**
  - `appointment_id` (Primary Key) – Unique identifier for each appointment.
  - `date` – Date of the appointment.
  - `patient_id` (Foreign Key) – Links to the patient table.
  - `doctor_id` (Foreign Key) – Links to the doctor table.

### **4. Billing Table (`billing`)**
- **Columns:**
  - `invoice_id` (Primary Key) – Unique billing identifier.
  - `patient_id` (Foreign Key) – Links to the patient table.
  - `procedure_name` – Name of the medical procedure billed.
  - `amount` – Billing amount in cents.

### **5. Medical Procedure Table (`medical_procedure`)**
- **Columns:**
  - `procedure_id` (Primary Key) – Unique procedure identifier.
  - `procedure_name` – Name of the medical procedure.
  - `appointment_id` (Foreign Key) – Links to the appointment table.

---

## **Project Workflow & Cleaning Process**

### **Data Cleaning:**
- Ordered each table by its respective primary key (`patient_id`, `doctor_id`, etc.).
- Identified duplicate IDs across all tables.
- Used `ROW_NUMBER()` to generate new unique IDs where necessary.
- Updated linked tables to maintain referential integrity.

#### **Patient Table Cleaning:**
- Found multiple patients sharing the same ID.
- Used `ROW_NUMBER()` to assign new unique IDs starting at 100.
- Updated `patient_id` in the `appointment` and `billing` tables.

#### **Doctor Table Cleaning:**
- Found multiple doctors sharing the same ID.
- Used `ROW_NUMBER()` to assign new unique IDs starting at 100.
- Updated `doctor_id` in the `appointment` table.
- Created unique doctor contact emails.

#### **Appointment Table Cleaning:**
- Identified duplicate `appointment_id` values.
- Used `ROW_NUMBER()` to create new unique `appointment_id` values.
- Updated linked `appointment_id` values in the `medical_procedure` table.
- Removed the `time` column due to incorrect data.

#### **Billing Table Cleaning:**
- Checked for missing `invoice_id` values before proceeding.
- Changed `amount` from dollars to cents to maintain consistency.

#### **Medical Procedure Table Cleaning:**
- Identified duplicate `procedure_id` values and reassigned new ones.
- Verified all `appointment_id` links matched the cleaned `appointment` table.

---

## **Data Integrity Issues**
During revenue analysis, incorrect results were found:
- Revenue was highest for patients with **zero** appointments and lowest for those with **six** appointments.
- Investigation revealed missing billing and appointment records, which could not be verified.
- Due to these inconsistencies, financial analysis was **excluded** from the project.

Additional integrity findings:
- **257 patients** had **appointments but no billing records**.
- **169 patients** had **billing records but no appointments**.
- No orphaned billing or appointment records were found.

---

## **Key Findings**

### **Patient Insights**
- **999 unique patients**.
- **Appointments per year**:
  - **2020:** 261
  - **2021:** 247
  - **2022:** 239
  - **2023:** 253
- **Appointments by day**:
  - **Most:** Friday (157)
  - **Least:** Saturday (134)
- **Appointments by month**:
  - **Most:** January (97)
  - **Least:** March (77)

### **Doctor Insights**
- **999 unique doctors** across **24 specialties**.
- **Doctors per number of appointments**:
  - 388 had **0** appointments.
  - 342 had **1** appointment.
  - 180 had **2** appointments.
  - Only **3** doctors had **5+** appointments.
- **Top 3 Specialties**:
  - Otolaryngologists: **62** appointments
  - Oncologists: **60** appointments
  - Pediatrics: **57** appointments

### **Procedure Insights**
- **Total procedures recorded:** **1,000**
- **Most common procedures (22.8% of all procedures):**
  - **X-rays, CT scans, MRI scans:** 26 occurrences
  - **Coronary artery bypass surgery:** 25 occurrences
  - **Comprehensive geriatric assessment:** 24 occurrences

---

## **Conclusion & Recommendations**
**1. Improve Data Integrity**
- Ensure billing records match appointments.
- Standardize patient-doctor links to avoid mislinked records.

**2. Optimize Appointment Scheduling**
- Friday is the busiest day—consider redistributing appointments for efficiency.

**3. Address Doctor Workload**
- Over 38% of doctors have **zero** appointments—re-evaluate staffing needs.

-Feel free to explore the queries and datasets in the repository.


