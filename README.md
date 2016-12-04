# Fourth_question

In this question I have used Hivae and Pig.

Here need to find out the Departments, Department numbers, manager of each department, CTC (sum of salary of all employees under each department and manager) and Total number of employees under each department and manager.

Here I have used below Hive query to get the Department wise department number, name of department, department manager, CTC (sum) of salry of total number of emplyees under perticualr department and Total number of employee under each department.

Query as:

INSERT OVERWRITE LOCAL DIRECTORY '/home/vishnu/Documents/New_depts_d005' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments1 as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd005' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

-- Here In above query I have used join on multiple table to get the department number, Department name, Manager name, CTC as salary of employes under that department, and total number of employee under each department and this data I have stored in CSV file as mentioned in above query using insert statement.

Now I have used Pig , and used above generated CSV file in Pig.

In pig I have processed generated data and get the Sum of salary of all employee under each department along with required all column as output.

Pig Script as:

employee_dept_details = LOAD '/home/vishal/Downloads/d005/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
student_workpages_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE student_workpages_sum INTO 'file:///home/vishal/Desktop/d004';

Here in above script, I am loading the CSV file generated file in hive and then processing on this file and getting the sum of salari department wise with Department name, number, Manager name, CTC and Total number of employee of each department.


File Details as:




