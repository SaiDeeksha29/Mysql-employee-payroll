# Mysql-employee-payroll
## UC1 - Create database for payroll_service
```create database payroll_service;```

### See the DB created using show database query
```show databases;```

### Go to the database created
```use payroll_service;```

## UC2 - create a employee payroll table
```
CREATE TABLE employee_payroll
    -> (
    ->   id                  INT unsigned NOT NULL AUTO_INCREMENT,
    ->   name                VARCHAR(150) NOT NULL,
    ->   salary              Double NOT NULL,
    ->   start               DATE NOT NULL,
    ->   PRIMARY KEY         (id)
    -> );
```

### See the table by using database query
```DESCRIBE employee_payroll;```

## UC3 - Ability to create employee payroll data in the payroll service
```
 INSERT INTO employee_payroll(name , salary , start) VALUES
    -> ( 'Bill',1000000.00,'2018-01-03'),
    -> ( 'Terisa',2000000.00,'2019-11-13'),
    -> ('Charlie',3000000.00,'2020-05-21');
```

## UC4 - Ability to retrieve all the employee payroll
```SELECT* FROM employee_payroll;```

## UC5 - Ability to retrieve salary of particular person and employees who have joined in a particular data range

### Viewing salary of particular person
```SELECT salary FROM employee_payroll WHERE name='Charlie';```

### Checking employees who joined at particular date range
```SELECT * FROM employee_payroll WHERE start BETWEEN CAST('2019-01-01' AS DATE) AND DATE(NOW());```

## UC6- Ability to add gender to table

### Adding gender
```ALTER TABLE employee_payroll ADD gender CHAR(1) AFTER name;```

### Setting F gender for female employees
```update employee_payroll set gender = 'F' where name='Terisa' or name='Deeksha';```

### Setting M gender for male employees
```update employee_payroll set gender='M' where name='Bill' or name='Charlie';```

### Viewing gender
```SELECT * FROM employee_payroll;```

## UC7 - Ability to Find Sum,Average,Min,Max,Count

### Total salary according to gender
```SELECT gender, SUM(salary) FROM employee_payroll GROUP BY gender;```

### Average salary according to gender
```SELECT gender, AVG(salary) FROM employee_payroll GROUP BY gender;```

### Minimum salary according to gender
```SELECT gender, MIN(salary) FROM employee_payroll GROUP BY gender;```

### Maximum salary according to gender
```SELECT gender, MAX(salary) FROM employee_payroll GROUP BY gender;```

### Count of employees according to gender
```SELECT gender, COUNT(salary) FROM employee_payroll GROUP BY gender;```

## UC8 - Ability to extend employee_payroll data to store employee information like employee phone, address and department

### Adding phone number to table after name
```
ALTER TABLE employee_payroll ADD phone_number VARCHAR(250) AFTER name;
```

### Adding address to table after phone number
```
ALTER TABLE employee_payroll ADD address VARCHAR(250) AFTER phone_number;
```

### Adding department after address
```
ALTER TABLE employee_payroll ADD department VARCHAR(150) NOT NULL AFTER address;
```

### Setting default value for address
```
ALTER TABLE employee_payroll ALTER address SET DEFAULT 'TBD';
```

## UC9 -Ability to extend employee_payroll table to have Basic Pay, Deductions, Taxable Pay, Income Tax, Net Pay

### Changing salary column name to basic_pay
```ALTER TABLE employee_payroll RENAME COLUMN salary TO basic_pay;```

### Adding deductions after basic_pay
```ALTER TABLE employee_payroll ADD deductions Double NOT NULL AFTER basic_pay;```

### Adding taxable_pay after deductions
```ALTER TABLE employee_payroll ADD taxable_pay Double NOT NULL AFTER deductions;```

### Adding tax after taxable_pay
```ALTER TABLE employee_payroll ADD tax Double NOT NULL AFTER taxable_pay;```

### Adding net_pay after tax
```ALTER TABLE employee_payroll ADD net_pay Double NOT NULL AFTER tax;```

## UC10.1 - Ability to make Terisa as a part of Sales and Marketing Department

```
update employee_payroll set department='Sales' where name='Terisa';
insert into employee_payroll (name, department, gender, basic_pay, deductions, taxable_pay, tax, net_pay, start)
VALUES('Terisa', 'Marketing', 'F', 200000.00, 50000.00, 150000.00, 50000.00, 100000.00, '2018-01-03');
``` 

## UC11 - Implement ER diagram
### Creating table company
```
(
-> company_ID  INT PRIMARY KEY,
-> company_Name varchar(150) NOT NULL
-> )ENGINE=INNODB;
```

### Creating table employee
```
CREATE TABLE employee
-> (
-> ID   INT unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
-> company_ID INT,
-> phone_number    varchar(250),
-> address         varchar(250),
-> gender          char(1),
-> Name            varchar(150) NOT NULL,
-> FOREIGN KEY (company_ID) REFERENCES company (company_ID)
-> )ENGINE=INNODB;
```

### Creating table payroll
```
CREATE TABLE payroll
-> (
-> ID   INT unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
-> FOREIGN KEY (ID) REFERENCES employee (ID),
-> basic_pay    DOUBLE NOT NULL,
-> deductions   DOUBLE NOT NULL,
-> taxable_pay  DOUBLE NOT NULL,
-> tax          DOUBLE NOT NULL,
-> net_pay      DOUBLE NOT NULL
-> )ENGINE=INNODB;
```

### Creating table department
```
CREATE TABLE department(
-> Department_ID int NOT NULL PRIMARY KEY,
-> Department_Name varchar(150) NOT NULL
-> )ENGINE=INNODB;
```

### Creating table employee_department
```
create table employee_department(
-> ID   INT unsigned NOT NULL AUTO_INCREMENT,
-> FOREIGN KEY (ID) REFERENCES employee (ID),
-> Department_ID int NOT NULL,
-> FOREIGN KEY (Department_ID) REFERENCES department (Department_ID)
-> )ENGINE=INNODB;
```

## UC12 - Ensure all retrieve queries done
### Inserting into company table
```
INSERT INTO company VALUES
    -> (1,'Capgemini'),
    -> (2,'Microsoft'),
    -> (3,'Reliance');
```

### Inserting into employee table
```
INSERT INTO employee VALUES
    -> (101,1,'8886771','Hyderabad','F','Deeksha'),
    -> (102,2,'4567823','Chennai','F','Kavya'),
    -> (103,3,'4567828','Pune','M','Karthik');
```

### Inserting into payroll table
```
INSERT INTO payroll VALUES
    -> (101,50000,5000,45000,5000,40000),
    -> (102,20000,2000,18000,3000,15000),
    -> (103,60000,6000,54000,4000,50000);
```

### Inserting into department table
```
INSERT INTO department VALUES
    -> (21,'AI'),
    -> (22,'CSE'),
    -> (23,'Sales and Marketing');
```

### Inserting into employee_department table
```
INSERT INTO employee_department VALUES
    -> (101,21),
    -> (102,22),
    -> (103,23),
    -> (102,21);
```

### Altering payroll table to add start date and insert values
```
ALTER TABLE payroll ADD start DATE;
UPDATE payroll set start = '2019-10-12' where id=102;
UPDATE payroll set start = '2018-1-15' where id=101;
UPDATE payroll set start = '2018-5-9' where id=103;
SELECT * from payroll where start between CAST('2019-1-1' AS DATE) and DATE(NOW());
```

### Total salary according to gender
```
select sum(p.net_pay),e.gender from employee e left join payroll p on p.ID=e.ID group by e.gender;
```

### Average salary according to gender
```
select avg(p.net_pay),e.gender from employee e left join payroll p on p.ID=e.ID group by e.gender;
```

### Minimum salary according to gender
```
select min(p.net_pay),e.gender from employee e left join payroll p on p.ID=e.ID group by e.gender;
```

### Maximum salary according to gender
```
select max(p.net_pay),e.gender from employee e left join payroll p on p.ID=e.ID group by e.gender;
```

### Count of employees according to gender
```
select count(p.net_pay),e.gender from employee e left join payroll p on p.ID=e.ID group by e.gender;
```
