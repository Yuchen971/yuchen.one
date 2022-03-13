- Lecture Notes (Modules)
	- [[Introduction to Data Structures]]
	- [[Relational Database Design]]
	- [[Relational Database Programming (SQL)]]
	- [[Data Warehousing]]
-
- Assignments
	- DONE HW3 11:00 PM
	  :LOGBOOK:
	  CLOCK: [2022-02-25 Fri 15:58:26]--[2022-02-25 Fri 20:22:14] =>  04:23:48
	  :END:
	- DONE HW4
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2022-03-10 Thu 15:12:55]--[2022-03-10 Thu 15:12:56] =>  00:00:01
	  CLOCK: [2022-03-10 Thu 15:12:57]--[2022-03-10 Thu 15:13:02] =>  00:00:05
	  :END:
		- Problem 1: Data Warehouse Design
			- International Foods Logical Data Model
			  collapsed:: true
				- ![CleanShot_Module 4 Homework (page 3  17)_20220304.png](../assets/CleanShot_Module_4_Homework_(page_3_17)_20220304_1646446406639_0.png)
			- You wish to design a sales DataMart for International Foods. Your sales business users wish to be able to ask questions such as:
			  collapsed:: true
				- What was the total ==revenue== by ==product== for a specific ==day== (Monday, Tuesday, .../month (1-12)/ week (1-52) /year?
				- What was the total ==revenue== by ==category== for a specific ==day==/month/ week/year?
				- How much did each ==customer== purchase (==quantity== or ==price==) by ==product== or by ==category==?
				- Which ==products== were ==discounted== the most often?
				- What was the total ==revenue== by ==customer city? country==?
				- What was the total ==revenue== by employee? By ==employee city? country?==
				- What was the total ==quantity== shipped by ==shipper==? Total quantity of a specific ==product== ==category== by ==shipper==:
			- 1A) Answer the following questions
			  background-color:: #793e3e
				- What is the grain?
					- each row represents a single product on a single order detail
				- What are the dimensions?
				- What are the facts?
			- 1B) draw the star schema
			  background-color:: #793e3e
			- 1C) For the facts in your Sales DataMart, indicate whether they are fully additive, semi-additive, or non-additive. For any semi-additive facts, indicate the dimensions that they cannot be added across.
			  background-color:: #793e3e
				- revenue: fully additive
				- discontinued: non-additive
				- order_quantity:  fully additive
			- ---
			- You now wish to design a suppler DataMart for International Foods.
			  Your supplier management business users wish to be able to ask questions such as:
				- What was the ==total quantity== by ==product== supplied for a specific ==supplier== for a specific ==day/month/ week/year==?
				- What was the ==total quantity== by ==category== by ==supplier== a specific ==date==/day of week/month/ week/year?
				- What was the ==total quantity== ordered by ==supplier city? supplier country?==
			- 1D) Answer the following questions
			  background-color:: #793e3e
				- What is the grain?
					- each row represent single product with single supplier
				- What are the dimensions?
					- date, product, supplier, order
				- What are the facts?
					- supplied quantity
			- 1E) Which dimensions should conformed the two DataMarts?
			  background-color:: #793e3e
				- Date, Product
			- 1F) draw star schema
			  background-color:: #793e3e
				- see P1.drawio
			- 1G) For the facts in your Supplier DataMart, indicate whether they are fully additive, semi-additive, or non-additive. For any semi-additive facts, indicate the dimensions that they cannot be added across.
			  background-color:: #793e3e
				- supplied quantity: fully additive
			- 1H) Draw the data model of your proposed Data Warehouse consisting of your two DataMarts and showing their conformed dimensions
			  background-color:: #793e3e
				- see P1.drawio
		- Problem 2: Telephone Provider Data Warehouse
			- You work for a telephone provider that wishes to design a datamart to report on and analyze its call data. They would like to be able to answer questions and queries such as:
				- What was the total ==amount== collected by each ==call program== in ==2012==?
				- What was the total ==duration of calls== made by ==customers== in ==Brazil== in 2014?
				- What was the ==total number of weekend calls== made by ==customers== from Brussels to customers in Antwerp in 2012?
				- What was the total duration of ==international calls== started by customers in Belgium in 2012?
				- What was the total amount collected from customers in Brussels who ==enrolled== in the "corporate" ==program== in 2012?
			- 2A) Answer the following questions
			  background-color:: #793e3e
				- What is the grain?
					- each row represents a single call from a single customer
				- What are the dimensions?
				- What are the facts?
			- 2B) Draw the data model of your proposed DataMart (star schema). For full credit, include the primary and foreign keys. You do not need to list all the attributes of the dimension tables but be sure to list all the attributes needed to answer the business questions on the previous page.
			  background-color:: #793e3e
			- 2C) For the facts in your Sales DataMart, indicate whether they are fully additive, semi-additive, or non-additive. For any semi-additive facts, indicate the dimensions that they cannot be added across.
			  background-color:: #793e3e