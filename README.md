# **Pagila Data Warehouse & ETL Exercise🧩**
Hi✋.This is a tutorial for the PostgreSQL exercise using the Pagila dataset. I'll try to take you through it step by step, explaining howerver I can🙂. Try to follow and understand the concept, don't just copy the code. Let's go🏃‍♂️🏃‍♂️
## Prerequisites
### 1. Verify PostgreSQL is installed
You must have PostgreSQL installed on your machine to do this exercise. To check is you have Postgres running;  
*  Open **Terminal/Command prompt** and type **psql --version** and press **Enter**
*  You should see something like **psql (PostgreSQL) 18.3**
      
If you get an error then either Postgres wasn't installed properly or you need to add Postgres to **System Environment Variables**.  
If Postgres wasn't installed properly, uninstall it and remove all traces of it by deleting its file directory (It's usually located in  
**C:\Program Files\PostgreSQL**).  
Then reinstall it, this time following the steps carefully. You can find the installation guide in: https://www.postgresql.org/docs/current/tutorial-install.html  
Then add it to **Path Environment variables** (This applies also if it's installed correctly and **psql --version** gives an error message!)
* Navigate to the directory where PostgreSQL is installed, usually **C:\Program Files\PostgreSQL** and navigate to the bin folder.
  
  <img width="600" height="250" alt="navigate to directory" src="https://github.com/user-attachments/assets/08ee0551-b127-4528-811b-8995408b26cd" />
* Double click the address bar and **copy the path**.
  
  <img width="560" height="280" alt="copy path" src="https://github.com/user-attachments/assets/bb787977-8d60-45c0-824f-16c5cec9364c" />
* Click the Windows Search icon and search **Edit system environment variables**. Alternatively **Press Win + R** and type **SystemPropertiesAdvanced** then press **Enter**.
* Click **Environment Variables** to open environment variables window.
  
  <img width="400" height="400" alt="edit system env" src="https://github.com/user-attachments/assets/b3efcdee-4824-4c50-9253-87228cc659a9" />
* Select **Path** on the system environment variables and click **Edit**.
  
  <img width="512" height="500" alt="edit path" src="https://github.com/user-attachments/assets/afecbdb4-47b8-463a-8d24-af6fab70088e" />
* In the edit window, click **New** and Paste the path you copied earlier. Save the changes. **🚫Note: Don't close the window by clicking the close button on top right. Just click OK until you exit the entire process**.

  <img width="500" height="400" alt="added path" src="https://github.com/user-attachments/assets/acc43e60-9fbf-4ad5-8896-fa84ae4c3cdb" />
* Restart the **Terminal** and now when you type **psql --version** you should see **psql (PostgreSQL) 18.3**.

### 2. Dashboard GUI
This guide strictly uses pgAdmin 4 (which usually comes bundled with PostgreSQL).

## The Exercise
In the exercise you are required to perform the **ETL** process for a **Data Warehouse** from OLTP tables. 

>The exercise was as follows:
>Create 

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

The schema and the dataset can be downloaded as a Zip file in Kaggle here 👉https://www.kaggle.com/datasets/kapturovalexander/pagila-postgresql-sample-database . **Note: You may need to create an account to be able to download the file**.

  <img width="700" height="283" alt="pagila" src="https://github.com/user-attachments/assets/313adb29-2ee9-493c-969f-9cacf633f40e" />  

  
Once you've downloaded it, extract the files. It containts a number of sql files e.g. pagila-schema.sql, pagila-insert-data.sql etc.  
✅You'll also need the queries for creating the data warehouse, download the **dw** file in this repo and extract it.

  

