# Mysql-employee-payroll
## UC1 - Create database for payroll_service
```create database payroll_service;```

### See the DB created using show database query
```show databases;```

### Go to the database created
```use payroll_service;```

## UC2 - create a employee payroll table
```CREATE TABLE employee_payroll
    -> (
    ->   id                  INT unsigned NOT NULL AUTO_INCREMENT,
    ->   name                VARCHAR(150) NOT NULL,
    ->   salary              Double NOT NULL,
    ->   start               DATE NOT NULL,
    ->   PRIMARY KEY         (id)
    -> );```

### See the table by using database query
```DESCRIBE employee_payroll;```

