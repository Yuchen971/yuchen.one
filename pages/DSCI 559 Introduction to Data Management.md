- Lecture Notes (Modules)
	- [[Introduction to Data Structures]]
	- [[Relational Database Design]]
	- [[Relational Database Programming (SQL)]]
	- [[Data Warehousing]]
	- [[Data Mart]]
	-
- DONE HW_5A HW5 [[2022-04-04 Monday]] 11:59PM
  collapsed:: true
	- dimension tables
		- supplier_dim
		  collapsed:: true
			- create
			  collapsed:: true
				- ```sql
				    CREATE TABLE International_Foods_warehouse.supplier_dim(
				      supplier_id INT PRIMARY KEY,
				      supplier_name VARCHER (8000),
				      supplier_city VARCHER (8000),
				      supplier_country VARCHER (8000)
				  )
				  ```
			- populate
			  collapsed:: true
				- supplier name is the company name or contact name
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.supplier_dim(
				          supplier_id,
				          supplier_name,
				          supplier_city,
				          supplier_country
				      )
				  SELECT
				      s.id,
				      s.CompanyName,
				      s.City,
				      s.Country
				  FROM
				      International_Foods.supplier s
				  ```
		- date_dim
		  collapsed:: true
			- create
			  collapsed:: true
				- ```sql
				  CREATE TABLE International_Foods_warehouse.date_dim (
				    date VARCHAR (8000) PRIMARY KEY,
				    week INT,
				    month INT,
				    year INT
				  )
				  ```
			- populate
			  collapsed:: true
				- date using order date
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.date_dim(date, week, month, year)
				  SELECT
				      DISTINCT date(OrderDate),
				      strftime('%w', OrderDate),
				      strftime('%m', OrderDate),
				      strftime ('%Y', OrderDate)
				  FROM
				      International_Foods.Orders;
				  ```
		- product_dim
		  collapsed:: true
			- create
				- ```sql
				  CREATE TABLE International_Foods_warehouse.product_dim (
				      product_id INT PRIMARY KEY,
				      product_name VARCHAR (8000),
				      category_name VARCHAR (8000)
				  )
				  ```
			- populate
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.product_dim(
				          product_id,
				          product_name,
				          category_name
				      )
				  SELECT
				      p.Id,
				      p.ProductName,
				      c.CategoryName
				  FROM
				      International_Foods.Product p
				      LEFT JOIN Category c ON c.Id = p.CategoryId
				  ```
		- customer_dim
		  collapsed:: true
			- create
				- customer id is varchar
				- ```sql
				  CREATE TABLE International_Foods_warehouse.customer_dim (
				      customer_id VARCHAR (8000) PRIMARY KEY,
				      customer_name VARCHAR (8000),
				      customer_country VARCHAR (8000)
				  )
				  ```
			- populate
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.customer_dim(
				          customer_id,
				          customer_name,
				          customer_country
				      )
				  SELECT
				      c.Id,
				      c.CompanyName,
				      c.Country
				  FROM
				      International_Foods.Customer c
				  ```
		- shipper_dim
		  collapsed:: true
			- create
				- ```sql
				  CREATE TABLE International_Foods_warehouse.shipper_dim (
				      shipper_id INT PRIMARY KEY,
				      company_name VARCHAR (8000)
				  )
				  ```
			- populate
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.shipper_dim(
				          shipper_id,
				          company_name
				      )
				  SELECT
				      s.Id,
				      s.CompanyName
				  FROM
				      International_Foods.Shipper s
				  ```
		- employee_dim
		  collapsed:: true
			- create
				- ```sql
				  CREATE TABLE International_Foods_warehouse.employee_dim (
				      employee_id INT PRIMARY KEY,
				      employee_last_name VARCHAR (8000),
				      employee_first_name VARCHAR (8000),
				      employee_city VARCHAR (8000),
				      employee_country VARCHAR (8000)
				  )
				  ```
			- populate
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.employee_dim(
				          employee_id,
				          employee_last_name,
				          employee_first_name,
				          employee_city,
				          employee_country
				      )
				  SELECT
				      e.Id,
				      e.LastName,
				      e.FirstName,
				      e.City,
				      e.Country
				  FROM
				      International_Foods.Employee e
				  ```
	- fact tables
		- supplier_fact
		  collapsed:: true
			- create
				- ```sql
				  CREATE TABLE International_Foods_warehouse.supplier_fact(
				      date VARCHER (8000) REFERENCES date_dim (date),
				      product_id INT REFERENCES product_dim (product_id),
				      supplier_id INT REFERENCES supplier_dim (supplier_id),
				      quantity INT
				  )
				  ```
			- populate
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.supplier_fact(
				      date,
				      product_id,
				      supplier_id,
				      quantity
				      )
				  SELECT
				      DATE(o.OrderDate),
				      od.ProductId,
				      p.SupplierID,
				      od.Quantity
				  FROM
				      International_Foods.Orders o
				      LEFT JOIN International_Foods.OrderDetail od ON od.OrderID = o.Id
				      LEFT JOIN International_Foods.Product p on p.Id = od.ProductId
				  ```
		- sales_fact
		  collapsed:: true
			- create
			  collapsed:: true
				- ```sql
				  CREATE TABLE International_Foods_warehouse.sales_fact(
				      date VARCHER (8000) REFERENCES date_dim (date),
				      product_id INT REFERENCES product_dim (product_id),
				      customer_id VARCHER (8000) REFERENCES customer_dim (customer_id),
				      shipper_id INT REFERENCES shipper_dim (shipper_id),
				      employee_id INT REFERENCES employee_dim (employee_id),
				      unit_price DECIMAL,
				      quantity INT,
				      discount DOUBLE,
				      total_revenue DECIMAL
				  )
				  ```
			- populate
			  collapsed:: true
				- ```sql
				  INSERT INTO
				      International_Foods_warehouse.sales_fact(
				      date,
				      product_id,
				      customer_id,
				      shipper_id,
				      employee_id,
				      unit_price,
				      quantity,
				      discount,
				      total_revenue
				      )
				  SELECT
				      DATE(o.OrderDate),
				      od.ProductId,
				      c.Id,
				      o.ShipVia, /* shipper id*/
				      o.EmployeeId,
				      od.UnitPrice,
				      od.Quantity,
				      od.Discount,
				      od.UnitPrice*od.Quantity*(1-od.Discount)
				  FROM
				      International_Foods.Orders o
				      LEFT JOIN International_Foods.OrderDetail od ON od.OrderID = o.Id
				      LEFT JOIN International_Foods.Product p ON p.Id = od.ProductId
				      LEFT JOIN International_Foods.Customer c ON c.Id = o.CustomerId
				  ```
			-
	- Questions
		- What was the total revenue for Tofu during July 2013?
		  collapsed:: true
			- ```sql
			  SELECT
			      SUM(total_revenue),
			      year,
			      month,
			      product_name
			  FROM
			      sales_fact s
			      LEFT JOIN product_dim p ON p.product_id = s.product_id
			      LEFT JOIN date_dim d ON d.date = s.date
			  WHERE
			      YEAR = 2013
			      AND MONTH = 7
			      AND product_name = 'Tofu'
			  ```
		- What was the average sales of Ipoh Coffee by day of the week during 2014?
		  collapsed:: true
			- ```sql
			  SELECT
			      AVG(total_revenue) as avg_revenue,
			      AVG(quantity) as avg_quantity,
			      year,
			      week
			  FROM
			      sales_fact s
			      LEFT JOIN date_dim d ON d.date = s.date
			      LEFT JOIN product_dim p ON p.product_id = s.product_id
			  WHERE
			      d.year = 2014 and p.product_name = "Ipoh Coffee"
			  GROUP BY
			      week
			  ```
-