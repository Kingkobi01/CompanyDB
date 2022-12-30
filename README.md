# Creating the Company database
[See Schema PDF](./company-database.pdf--)

## Creating the `Employee` table

```sql
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(40) NOT NULL,
    last_name VARCHAR(40) NOT NULL,
    birth_date DATE,
    sex VARCHAR(1),
    salary INT,
    super_id INT ,
    branch_id INT
);
```

## Creating the `Branch` Table

```sql
CREATE Table Branch (
    branch_id INT PRIMARY KEY AUTO_INCREMENT,
    branch_name VARCHAR(20) UNIQUE,
    mgr_id INT,
    mgr_start_date DATE
);
```

## Creating the `Client` Table

```sql
CREATE TABLE Client (
    client_id INT PRIMARY KEY AUTO_INCREMENT,
    client_name VARCHAR(30) UNIQUE,
    branch_id INT
);
```

## Creating the `Works_With` Table

```sql
CREATE TABLE Work_With (
    emp_id INT ,
    client_id INT,
    total_sales INT
);
```

## Creating the `Branch_Supplier` Table

```sql
CREATE TABLE Branch_Supplier (
    branch_id INT,
    supplier_name VARCHAR(30),
    supply_type VARCHAR(20)
);
```
