# **Pagila Data Warehouse & ETL Exercise🧩**
Hi✋.This is a tutorial for the PostgreSQL exercise using the Pagila dataset. I'll try to take you through it step by step, explaining the best way I can🙂. Try to follow and understand the concept, don't just copy the code. Let's go🏃‍♂️🏃‍♂️
## Prerequisites
### 1. Verify PostgreSQL is installed
You must have PostgreSQL installed on your machine to do this exercise. To check if you have Postgres running in your machine;  
*  Open **Terminal/Command prompt** and type **psql --version** and press **Enter**
*  You should see something like **psql (PostgreSQL) 18.3**
      
If you get an error, then either Postgres wasn't installed properly or you need to add Postgres to **System Environment Variables**.  
If Postgres wasn't installed properly, uninstall it and remove all traces of it by deleting its file directory (It's usually located in **C:\Program Files\PostgreSQL**).  
Then **reinstall** it, this time following the steps carefully. You can find the installation guide in: https://www.postgresql.org/docs/current/tutorial-install.html  
Then add it to **Path Environment variables**. (This also applies if it's installed correctly and **psql --version** gives an **error message**)
* Navigate to the directory where PostgreSQL is installed, usually **C:\Program Files\PostgreSQL** and navigate to the **bin** folder.
  
  <img width="600" height="250" alt="navigate to directory" src="https://github.com/user-attachments/assets/08ee0551-b127-4528-811b-8995408b26cd" />
* Double click the **address bar** and **copy the path**.
  
  <img width="560" height="280" alt="copy path" src="https://github.com/user-attachments/assets/bb787977-8d60-45c0-824f-16c5cec9364c" />
* Click the Windows **Search icon** and search **Edit system environment variables**. Alternatively **Press Win + R** and type **SystemPropertiesAdvanced** then press **Enter**.
* Click **Environment Variables** to open environment variables window.
  
  <img width="400" height="400" alt="edit system env" src="https://github.com/user-attachments/assets/b3efcdee-4824-4c50-9253-87228cc659a9" />
* Select **Path** on the system variables and click **Edit**.
  
  <img width="512" height="500" alt="edit path" src="https://github.com/user-attachments/assets/afecbdb4-47b8-463a-8d24-af6fab70088e" />
* In the edit window, click **New** and Paste the path you copied earlier. Save the changes. **🚫Note: Don't close the window by clicking the close button on top right. Just click OK until you exit the entire process**.

  <img width="500" height="400" alt="added path" src="https://github.com/user-attachments/assets/acc43e60-9fbf-4ad5-8896-fa84ae4c3cdb" />
* Restart the **Terminal**. Now when you type **psql --version** you should see **psql (PostgreSQL) 18.3**.

### 2. Dashboard GUI
This guide strictly uses **pgAdmin 4** (which usually comes bundled with PostgreSQL).

## The Exercise
In the exercise you are required to perform the **ETL (Extract Transform Load)** process for a **Data Warehouse** from OLTP tables. 

>The exercise was as follows:

>Create: 

>**Fact Table: fact_rentals**
>* rental_id
>* customer_id
>* film_id
>* store_id
>* rental_date
>* return_date
>* amount

>**Dimension Tables:**
>* dim_customer
>* dim_film
>* dim_store
>* dim_date

>**Exercise 1**
>* Write SQL to extract and transform data from OLTP tables into DW tables.
>* Load data into the DW schema
>* Query the DW: Total revenue per store, Top 10 customers by spending, Monthly rental trends
>* Optimization  Techniques
>* Indexing, partitioning, Materialized views

The schema and the dataset can be downloaded as a Zip file from Kaggle here 👉https://www.kaggle.com/datasets/kapturovalexander/pagila-postgresql-sample-database . **Note: You may need to create an account to be able to download the file**.  
A class diagram is also provided, if you'd like to see the relationships within the database.

  <img width="700" height="283" alt="pagila" src="https://github.com/user-attachments/assets/313adb29-2ee9-493c-969f-9cacf633f40e" />  
  
Once you've downloaded it, extract the files. It containts a number of sql files e.g. **pagila-schema.sql, pagila-insert-data.sql etc**.  
✅You'll also need the queries for creating the data warehouse, download the **dw.zip** file in this repo and extract it.
**You are now ready!**
### 1. Step One: Set up the Transactional Database (OLTP)
First, we need to create our baseline database and load the raw DVD rental data.  
1. Open **pgAdmin 4** and connect to your local server.
2. Select **Databases** and right-click **Databases > Create > Database**.
   
   <img width="744" height="360" alt="create database" src="https://github.com/user-attachments/assets/4c423455-4ca8-42b2-92e3-3a6524d85c03" />
3. Name the database **pagila_dw_database** (or whatever you like really🙂) and **Save**.
4. Select your new **pagila_dw_database** and open the **Query Tool**.

   <img width="1105" height="422" alt="query tool" src="https://github.com/user-attachments/assets/caa69bd6-2392-4043-aab1-0087a7ad65e9" />
5. Open the files you downloaded from Kaggle and execute them, in a sequential order starting with **1.pagila-schema.sql** then **2.pagila-insert-data.sql** etc.

   <img width="1216" height="552" alt="execute queries" src="https://github.com/user-attachments/assets/94ce59bb-0c26-4541-b176-8ee4ffe21046" />
6. Once the query is pasted in the window, execute it. Repeat the process for all the query files.

   <img width="1157" height="502" alt="run" src="https://github.com/user-attachments/assets/c13d9aa5-489b-4fd1-b11c-e31324d76e2e" />

     
   >The **1.pagila-schema.sql** builds the database schema. **A schema** is a collection of logical structures that defines exactly how your analytical data is organized, stored, and related. Think of it as a **blueprint**. In contrast, a **Data Warehouse** is the entire storage system, basically, if the schema is a **floorplan** then the **DW** is the **building** itself.
   
   >A schema contains **Fact tables, Dimension tables, Data Types, Keys and Relationships, Constraints, Views, Indexes, and programmable objects like Stored Procedures, Functions and Triggers**.
   
   >A Data Warehouse on the other hand contains the **actual data**, **meta data** and the **computing power**.
   
   >The **2.pagila-insert-data.sql** adds data into our database.

   >There should be **pop-ups** below the query window when you execute the code informing you that the code compiled **successfully**. Alternatively, in the **Message panel** below the query window, there should be a message like `Successfully run. Total query runtime: 236 msec.
10 rows affected.`
   
   >You can query the database to check the data inserted, try `SELECT * FROM dw.dim_customer LIMIT 10;`. You should see results in the **Data Output panel**.
### 2. Step two: Create the Data Warehouse Schema (OLAP)
Now we build our warehouse separately to hold our denormalized **Dimension and Fact Tables**. Then we'll populate the **DW** with data from the **pagila_dw_database**.  
You should by now have the **dw.zip** provided in this repo, extracted. We'll start by defining the **DW** schema.  
1. Open the **dw** folder and run **dw_schema.sql**.
   
   <img width="1161" height="599" alt="dw schema" src="https://github.com/user-attachments/assets/db6d1d09-f3ed-4d28-abfc-a4f98d9f3db8" />

   >We've now build the schema, next we populate it with data.
2. Perform the same process, only this time execute the **insert queries**. Refresh your database tree. You should now see a **dw schema** containing tables like **dim_customer, dim_film, and fact_rentals**.

   <img width="700" height="700" alt="side panel" src="https://github.com/user-attachments/assets/de8a3b27-227f-4dd0-97e9-355eec8ad4ee" />


**Congratulations!💯🍾** And with that, the **pagila-dw-database** is complete. You can now answer and perform the analysis  mentioned in part 3 of the quizzes. I've provided the queries in the **dw** folder (the **quizzes** sub-folder), but you can try on your own if you'd like to practice😁.  
### Appendices
* **OLTP** - Online Transaction Processing
* **OLAP** - Online Analytical Processing
* **DW**   - Data Warehouse
* **SQL**  - Structured Query Language

## 🤝 Need Help or Found a Bug?
If you encounter any errors while running these scripts, or if you get stuck on the ETL phase:
* **Open an Issue**: Click on the **Issues tab** at the top of this repository and clearly describe the error message you are seeing. I will do my best to help you troubleshoot!
* **Contribute**: Did you find a better way to optimize one of the analytical queries? Feel free to fork this repository, add your improvements, and submit a **Pull Request**.

## ⭐ Support the Project
If this step-by-step guide helped you understand PostgreSQL Data Warehousing and the ETL process, please consider giving this repository a Star ⭐️ at the top right of the page. It helps others find this resource! It took me a lot of time to create this, any support is greatly appreciated😇.

Happy Querying! 🐘🚀


   



  

