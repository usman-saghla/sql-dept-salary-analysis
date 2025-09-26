# Department Salary Analysis (SQL)

This project provides an SQL query to analyze **average salaries across departments and genders** over time using the `employees_mod` database.  
The query aggregates salaries per year, department, and gender.

---

## 📂 Structure
- `queries/salary_analysis.sql` → Main SQL query
- `schema/` → (Optional) schema or table creation scripts if needed
- `samples/` → Example data and outputs

---

## 🛠️ Setup & Usage

1. Make sure you have the `employees_mod` schema available.  
   (This is a modified version of the standard MySQL Employees sample database.)

2. Run the query:

   ```sql
   USE employees_mod;

   SELECT
       e.gender,
       d.dept_name,
       ROUND(AVG(s.salary), 2) AS salary,
       YEAR(s.from_date) AS calendar_year
   FROM
       t_salaries s
   JOIN t_employees e ON s.emp_no = e.emp_no
   JOIN t_dept_emp de ON de.emp_no = e.emp_no
   JOIN t_departments d ON d.dept_no = de.dept_no
   GROUP BY d.dept_no, e.gender, calendar_year
   HAVING calendar_year <= 2002
   ORDER BY d.dept_no;
