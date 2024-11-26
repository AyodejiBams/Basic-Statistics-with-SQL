## Project Description

This project provides practical SQL queries to analyze statistical data, focusing on employee information and salary distribution. By leveraging SQL's analytical capabilities, this project explores data patterns, department performance, and salary trends within a company. These queries are useful for understanding fundamental SQL operations and applying statistical analysis to real-world datasets.

---

## Key Questions Addressed

### **1. Employee Overview**
- **Objective:** Understand the basic structure of the `staff` table and overall employee distribution.
- **Examples:**
  - View the first 5 rows of the `staff` table:
    ```sql
    SELECT * FROM staff LIMIT 5;
    ```
  - Count the total number of employees:
    ```sql
    SELECT COUNT(*) FROM staff;
    ```

---

### **2. Gender and Department Distribution**
- **Objective:** Analyze the gender and department-wise distribution of employees.
- **Examples:**
  - Gender distribution:
    ```sql
    SELECT gender, COUNT(*) AS total_employees
    FROM staff
    GROUP BY gender;
    ```
  - Number of employees in each department:
    ```sql
    SELECT department, COUNT(*) AS total_employee
    FROM staff
    GROUP BY department
    ORDER BY department;
    ```

---

### **3. Salary Analysis**
- **Objective:** Examine salary statistics, including minimum, maximum, average, and distribution.
- **Examples:**
  - Highest and lowest salaries in the company:
    ```sql
    SELECT MAX(salary) AS Max_Salary, MIN(salary) AS Min_Salary
    FROM staff;
    ```
  - Salary distribution by gender:
    ```sql
    SELECT gender, MIN(salary) AS Min_Salary, MAX(salary) AS Max_Salary, AVG(salary) AS Average_Salary
    FROM staff
    GROUP BY gender;
    ```
  - Total salary expenditure:
    ```sql
    SELECT SUM(salary)
    FROM staff;
    ```

---

### **4. Departmental Salary Insights**
- **Objective:** Analyze salary variations and spread across departments.
- **Examples:**
  - Department-wise salary distribution:
    ```sql
    SELECT
        department,
        MIN(salary) AS Min_Salary,
        MAX(salary) AS Max_Salary,
        AVG(salary) AS Average_Salary,
        COUNT(*) AS total_employees
    FROM staff
    GROUP BY department
    ORDER BY 4 DESC;
    ```
  - Department with the highest salary variance:
    ```sql
    SELECT 
        department, 
        MIN(salary) AS Min_Salary, 
        MAX(salary) AS Max_Salary, 
        ROUND(AVG(salary), 2) AS Average_Salary,
        ROUND(VAR_POP(salary), 2) AS Variance_Salary,
        ROUND(STDDEV_POP(salary), 2) AS StandardDev_Salary,
        COUNT(*) AS total_employees
    FROM staff
    GROUP BY department
    ORDER BY 6 DESC;
    ```

---

### **5. Bucket Analysis for Specific Departments**
- **Objective:** Classify employees into salary buckets (`high earner`, `middle earner`, `low earner`) and compare departments.
- **Examples:**
  - Create salary buckets for the Health department:
    ```sql
    CREATE VIEW health_dept_earning_status
    AS 
    SELECT 
        CASE
            WHEN salary >= 100000 THEN 'high earner'
            WHEN salary >= 50000 AND salary < 100000 THEN 'middle earner'
            ELSE 'low earner'
        END AS earning_status
    FROM staff
    WHERE department LIKE 'Health';
    ```
  - Compare bucket distributions:
    ```sql
    SELECT earning_status, COUNT(*)
    FROM health_dept_earning_status
    GROUP BY 1;
    ```

---

## Tools and Environment
- **Database Management Systems:** MySQL, PostgreSQL
- **Setup Requirements:**
  - Import the provided dataset into your database.
  - Execute the SQL queries sequentially to analyze the data.

---

## Learning Outcomes
- Understand how to use SQL for basic and advanced statistical analysis.
- Gain insights into employee data distribution and salary patterns.
- Apply SQL concepts like grouping, aggregation, and view creation.

---

## Acknowledgments
This repository is inspired by real-world data analytics scenarios to enhance SQL learning and problem-solving skills.
