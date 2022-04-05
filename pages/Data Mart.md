alias:: datamart

- 先根据star schema做出data warehouse, 然后 fully de-normalize 也就是数据全部整合到一起, 之后query data mart会简单很多
- Create warehouse [[ETL]] Example
	- Steps
	  collapsed:: true
		- Define and create the dimension tables
		- Define and create the fact table
		- Move the original entity table data into the dimension tables
		- Populate the fact table
	- [[star schema]]
	  collapsed:: true
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 50  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_50_117)_20220324_1648171935499_0.png)
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 77  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_77_117)_20220324_1648174842613_0.png)
		- combine with ER diagram
		  collapsed:: true
			- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 52  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_52_117)_20220324_1648172037662_0.png)
	- Create a new database
	  collapsed:: true
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 53  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_53_117)_20220324_1648172323405_0.png)
	- Store dimension table
	  collapsed:: true
		- Create
		  collapsed:: true
			- ```sql
			  CREATE TABLE sakila_data_warehouse.store_dim (
			      store_id INT PRIMARY KEY,
			      store_city VARCHAR (50),
			      store_country VARCHAR (50)
			  );
			  ```
		- Populate
		  collapsed:: true
			- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 55  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_55_117)_20220324_1648172370272_0.png)
			- ```sql
			  INSERT INTO
			      sakila_data_warehouse.store_dim(store_id, store_city, store_country)
			  SELECT
			      s.store_id,
			      c.city,
			      co.country
			  FROM
			      sakila.store s
			      LEFT JOIN sakila.address a ON s.address_id = a.address_id
			      LEFT JOIN sakila.city c ON a.city_id = c.city_id
			      LEFT JOIN sakila.country co ON c.country_id = co.country_id;
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 57  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_57_117)_20220324_1648172623138_0.png)
	- Film dimension table
	  collapsed:: true
		- Create
		  collapsed:: true
			- ```sql
			  CREATE TABLE sakila_data_warehouse.film_dim (
			      film_id INT PRIMARY KEY,
			      film_title VARCHAR (255),
			      film_category VARCHAR (25)
			  )
			  ```
		- Populate
		  collapsed:: true
			- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 59  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_59_117)_20220324_1648172695170_0.png)
			- ```sql
			  INSERT INTO
			      sakila_data_warehouse.film_dim(film_id, film_title, film_category)
			  SELECT
			      f.film_id,
			      f.title,
			      cat.name
			  FROM
			      sakila.film f
			      LEFT JOIN sakila.film_category fc ON f.film_id = fc.film_id
			      LEFT JOIN sakila.category cat ON cat.category_id = fc.category_id;
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 61  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_61_117)_20220324_1648172865869_0.png)
	- Customer dimension table
	  collapsed:: true
		- Create
		  collapsed:: true
			- ```sql
			  CREATE TABLE sakila_data_warehouse.customer_dim (
			      customer_id INT PRIMARY KEY,
			      customer_first_name VARCHAR (45),
			      customer_last_name VARCHAR (45),
			      customer_email VARCHAR (50),
			      customer_city VARCHAR (50),
			      customer_country VARCHAR (50)
			  )
			  ```
		- Populate
		  collapsed:: true
			- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 65  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_65_117)_20220324_1648173687001_0.png)
			- ```sql
			  INSERT INTO
			      sakila_data_warehouse.customer_dim(
			          customer_id,
			          customer_first_name,
			          customer_last_name,
			          customer_email,
			          customer_city,
			          customer_country
			      )
			  SELECT
			      cus.customer_id,
			      cus.first_name,
			      cus.last_name,
			      cus.email,
			      city.city,
			      country.country
			  FROM
			      sakila.customer cus
			      LEFT JOIN sakila.address addr ON cus.address_id = addr.address_id
			      LEFT JOIN sakila.city city ON addr.city_id = city.city_id
			      LEFT JOIN sakila.country country ON city.country_id = country.country_id;
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 67  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_67_117)_20220324_1648173801766_0.png)
	- Date dimension table
	  collapsed:: true
		- Create
		  collapsed:: true
			- ```sql
			  CREATE TABLE sakila_data_warehouse.date_dim (
			    date VARCHAR (12) PRIMARY KEY,
			    week INT,
			    month INT,
			    year INT
			  )
			  ```
		- Populate
		  collapsed:: true
			- collapsed:: true
			  ```sql
			  INSERT INTO
			      sakila_data_warehouse.date_dim(date, week, month, year)
			  SELECT
			      DISTINCT date(rental_date),
			      strftime('%W', rental_date),
			      strftime('%m', rental_date),
			      strftime ('%Y', rental_date)
			  FROM
			      sakila.rental;
			  ```
				- output
					- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 73  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_73_117)_20220324_1648174618355_0.png)
	- Rental fact table
	  collapsed:: true
		- Create
		  collapsed:: true
			- ```sql
			  CREATE TABLE sakila_data_warehouse.rentals_fact(
			      rental_id INT PRIMARY KEY,
			      film_id INT REFERENCES film_dim (film_id),
			      customer_id INT REFERENCES customer_dim (customer_id),
			      store_id INT REFERENCES store_dim (store_id),
			      date VARCHAR (12) REFERENCES date_dim (date),
			      amount INT
			  )
			  ```
		- Populate
		  collapsed:: true
			- ```sql
			  INSERT INTO
			      sakila_data_warehouse.rentals_fact (
			          rental_id,
			          film_id,
			          customer_id,
			          store_id,
			          date,
			          amount
			      )
			  SELECT
			      r.rental_id,
			      f.film_id,
			      c.customer_id,
			      s.store_id,
			      DATE(r.rental_date),
			      p.amount
			  FROM
			      sakila.rental r
			      LEFT JOIN sakila.payment p ON r.rental_id = p.rental_id
			      LEFT JOIN sakila.inventory i ON r.inventory_id = i.inventory_id
			      LEFT JOIN sakila.film f ON i.film_id = f.film_id
			      LEFT JOIN sakila.customer c ON r.customer_id = c.customer_id
			      LEFT JOIN sakila.store s ON i.store_id = s.store_id;
			  ```
				- output
				  collapsed:: true
					- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 76  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_76_117)_20220324_1648174778435_0.png)
- Create date mart (fully de-normalized)
	- Create Analytic-ready dataset from star schema
	  collapsed:: true
		- ```sql
		  CREATE TABLE sales_analytic_datamart.datamart (
		    rental_id INT PRIMARY KEY,
		    date VARCHAR (12),
		    week INT,
		    month INT,
		    year INT,
		    amount INT,
		    film_id INT,
		    film_title VARCHAR (255),
		    film_category VARCHAR (25),
		    customer_id INT,
		    customer_first_name VARCHAR (45),
		    customer_last_name VARCHAR (45),
		    customer_email VARCHAR (50),
		    customer_city VARCHAR (50),
		    customer_country VARCHAR (50),
		    store_id INT,
		    store_city VARCHAR (50),
		    store_country VARCHAR (50)
		  );
		  ```
		- ```sql
		  INSERT INTO
		      sales_analytic_datamart.datamart(
		          rental_id,
		          date,
		          week,
		          MONTH,
		          year,
		          amount,
		          film_id,
		          film_title,
		          film_category,
		          customer_id,
		          customer_first_name,
		          customer_last_name,
		          customer_email,
		          customer_city,
		          customer_country,
		          store_id,
		          store_city,
		          store_country
		      )
		  SELECT
		      r.rental_id,
		      d.date,
		      d.week,
		      d.month,
		      d.year,
		      r.amount,
		      f.film_id,
		      f.film_title,
		      f.film_category,
		      c.customer_id,
		      c.customer_first_name,
		      c.customer_last_name,
		      c.customer_email,
		      c.customer_city,
		      c.customer_country,
		      s.store_id,
		      s.store_city,
		      s.store_country
		  FROM
		      sakila_data_warehouse.rentals_fact r
		      LEFT JOIN sakila_data_warehouse.customer_dim c ON r.customer_id = c.customer_id
		      LEFT JOIN sakila_data_warehouse.date_dim d ON r.date = d.date
		      LEFT JOIN sakila_data_warehouse.film_dim f ON r.film_id = f.film_id
		      LEFT JOIN sakila_data_warehouse.store_dim s ON r.store_id = s.store_id;
		  ```
			- output
				- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 82  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_82_117)_20220324_1648175452292_0.png)
- Query example
	- Most frequently rented movies
	  collapsed:: true
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 84  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_84_117)_20220324_1648175807499_0.png)
	- Top five movies categories by revenue
	  collapsed:: true
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 85  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_85_117)_20220324_1648175833603_0.png)
	- Total sales by store with city and country
	  collapsed:: true
		- ![CleanShot_Module 5  Pt 1. - Data Preparation for Analytics (page 86  117)_20220324.png](../assets/CleanShot_Module_5_Pt_1._-_Data_Preparation_for_Analytics_(page_86_117)_20220324_1648175873536_0.png)
		-