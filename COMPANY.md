# Creating the Company database
[See Schema PDF](./company-database.pdf)

## Creating Tables

### Creating the `Employee` table

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

### Creating the `Branch` Table

```sql
CREATE Table Branch (
    branch_id INT PRIMARY KEY AUTO_INCREMENT,
    branch_name VARCHAR(20) UNIQUE,
    mgr_id INT,
    FOREIGN KEY(mgr_id) REFERENCES Employee(emp_id) ON DELETE SET NULL,
    mgr_start_date DATE
);
```

### Creating the `Client` Table

```sql
CREATE TABLE Client (
    client_id INT PRIMARY KEY AUTO_INCREMENT,
    client_name VARCHAR(30) UNIQUE,
    branch_id INT
);
```

### Creating the `Works_With` Table

```sql
CREATE TABLE Work_With (
    emp_id INT ,
    client_id INT,
    total_sales INT
);
```

### Creating the `Branch_Supplier` Table

```sql
CREATE TABLE Branch_Supplier (
    branch_id INT,
    supplier_name VARCHAR(30),
    supply_type VARCHAR(20)
);
```

### Now we make the `super_id` and `branch_id` foreignkeys to the `emp_id` of the `Employee` table and `branch_id` of the `Branch` table respectively.

```sql
ALTER TABLE `Employee`
ADD FOREIGN KEY (branch_id)
REFERENCES `Branch`(branch_id)
ON DELETE SET NULL;


ALTER TABLE `Employee`
ADD FOREIGN KEY (super_id)
REFERENCES `Employee`(emp_id)
ON DELETE SET NULL;
```

### Let's also make `branch_id` column of `Client` table a foreign_key to `branch_id` of `Branch` table

```sql
ALTER TABLE `Client`
ADD FOREIGN KEY (branch_id)
REFERENCES `Branch`(branch_id)
ON DELETE SET NULL
```

### Then we make both the `emp_id` and the `client_id` of `Work_With`primarykeys

```sql
ALTER TABLE `Work_With`
ADD PRIMARY KEY (emp_id, client_id);
```

### ...and we make them foreignkeys

```sql
ALTER TABLE `Work_With`
ADD FOREIGN KEY (client_id) REFERENCES `Client`(client_id) ON DELETE
CASCADE;

ALTER TABLE `Work_With`
ADD FOREIGN KEY (emp_id) REFERENCES `Employee`(emp_id) ON DELETE
CASCADE;
```

### Finally we make both the `branch_id` and the `supplier_name` of `Branch_Supplier` table primarykeys and make `branch_id` a foreignkey

```sql
ALTER TABLE `Branch_Supplier`
ADD PRIMARY KEY(branch_id, supplier_name);

ALTER TABLE `Branch_Supplier`
ADD FOREIGN KEY (branch_id) REFERENCES `Branch`(branch_id)
ON DELETE CASCADE;
```

## Populating Tables with data

