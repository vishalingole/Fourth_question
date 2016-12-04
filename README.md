# Fourth_question

In this question I have used Hive and Pig.

Here need to find out the Departments, Department numbers, manager of each department, CTC (sum of salary of all employees under each department and manager) and Total number of employees under each department and manager.

I have used below Hive query to get the Department wise department number, name of department, department manager,salary of employees who comes under particular department.

Please Find Details below:
# Final output is shown in the following format:
employee no,department_no,department name,manager name,CTC,Total number of employees

I have attached two zip files :
1) Question_four_hive_table_export_files.zip : Contains all the department wise csv genrated by HIVE which are used for further PIG operations.
2) Question_Four_output_csv_department_wise.zip : Contains all the department wise output files.

# Explanation of every steps:
* following HIVE query used to get data from hive table & genrate csv
1] INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d001' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd001' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

2] employee_dept_details = LOAD '/home/vishal/Downloads/d001/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int); //This steps loads the csv file from local path & genrate structure from it;

3] employee_group = Group employee_dept_details all; // This steps used to group all the data 
4] employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no); //This steps genrate the data in the provided format.
   
5] STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d002'; // This steps creates csv file of output.



# Please find below steps followed for output:
* Following HIVE query used to get employee details filter by department id i.e d001 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d001' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd001' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output.it takes csv file as input which is genrated by hive for processing.
employee_dept_details = LOAD '/home/vishal/Downloads/d001/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d001';

* Following HIVE query used to get employee details filter by department id i.e d002 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d002' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd002' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output.it takes csv file as input which is genrated by hive for processing.
employee_dept_details = LOAD '/home/vishal/Downloads/d002/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d002';


* Following HIVE query used to get employee details filter by department id i.e d003 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d003' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd003' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';


* Following PIG script is used to genrate desired output.it takes csv file as input which is genrated by hive for processing.
employee_dept_details = LOAD '/home/vishal/Downloads/d003/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d003';


* Following HIVE query used to get employee details filter by department id i.e d004 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d004' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd004' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d004/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
student_workpages_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE student_workpages_sum INTO 'file:///home/vishal/Desktop/d004';

* Following HIVE query used to get employee details filter by department id i.e d005 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d005' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd005' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d005/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d005';

* Following HIVE query used to get employee details filter by department id i.e d006 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d006' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd006' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d006/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d006';

* Following HIVE query used to get employee details filter by department id i.e d007 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d007' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd007' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d007/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d007';

* Following HIVE query used to get employee details filter by department id i.e d008 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d008' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd008' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d008/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d008';

* Following HIVE query used to get employee details filter by department id i.e d009 from multiple tables:
INSERT OVERWRITE LOCAL DIRECTORY '/home/vishal/Downloads/d009' row format delimited fields terminated by ',' select distinct(de.emp_no),de.dept_no,d.dept_name,e.first_name,dm.emp_no,s.salary from dept_manager as dm left join departments as d on (d.dept_no = dm.dept_no) LEFT JOIN dept_emp as de ON (de.dept_no = d.dept_no) left join salaries as s on (s.emp_no = de.emp_no) left join employees as e on (e.emp_no = dm.emp_no) where dm.dept_no = 'd009' AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01'AND s.to_date = '9999-01-01';

* Following PIG script is used to genrate desired output it takes csv file as input which is genrated by hive.
employee_dept_details = LOAD '/home/vishal/Downloads/d009/000000_0' USING PigStorage(',') as (emp_no:int,dept_no:chararray,dept_name:chararray,first_name:chararray,dmemp_no:int,salary:int);
employee_group = Group employee_dept_details all;
employee_salary_sum = foreach employee_group Generate 
   flatten(employee_dept_details),SUM(employee_dept_details.salary),COUNT(employee_dept_details.emp_no);
STORE employee_salary_sum INTO 'file:///home/vishal/Desktop/d009';



