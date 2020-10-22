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

###Viewing salary of particular person
```SELECT salary FROM employee_payroll WHERE name='Charlie';```

###Checking employees who joined at particular date range
```SELECT * FROM employee_payroll WHERE start BETWEEN CAST('2019-01-01' AS DATE) AND DATE(NOW());```

