# Crowdfunding_ETL

The project was undertaken as by Aadhithya Prakash and Daryl Pinto under the guidance of instructors at University of Toronto.

## Project Proposal:

The project focuses on building an Extract, Transform and load(ETL) pipeline using:
> Pandas
> 
> Python Dictionaries
> 
> SQL(Creating an ERD before creating the database in PostgreSQL)
> 

The deliverables for this project are as follows:
1. Create the Category and Subcategory DataFrames

2. Create the Campaign DataFrame

3. Create the Contacts DataFrame

4. Create the Crowdfunding Database


Work allocation:
> Both members collaborated together to write the code for Category and Subcategory Dataframes section.
>
> Daryl Pinto wrote the code for Campaign Dataframe section.
>
> Aadhithya Prakash wrote the code for Contacts Dataframe section.
>
> The ERD diagram along with the Crowdfunding Database was created by collaboration by both members.

The following sources of data were used in the project and can be found in the Resources Directory-
> [crowdfunding.xlsx](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Resources/crowdfunding.xlsx)
>
> [contacts.xlsx](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Resources/contacts.xlsx)

The final Database created is called Crowdfunding Database and is a relational database created with SQL.



## Project Report:
The project includes three aspects for database creations.
>Extract
>
>Transform
>
>Load

### Extract:
Initial Data to create the 'Category' and 'Subcategory' dataframes along with creating the 'campaign dataframe' was extracted from the excel file located in the Resources directory called - [crowdfunding.xlsx](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Resources/crowdfunding.xlsx) 

The Contacts Dataframe was created after extracting the excel file located in the Resources directory called - [contacts.xlsx](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Resources/contacts.xlsx)

### Transform:
In order to make the data viable for the final database. the following transformation processes were conducted:

1. Category and Subcategory Dataframes:
   
> 'Category & Subcategory' column located in the 'crowdfunding_info_df' dataframe was split on '/' to create the 'Category' and 'Subcategory' columns respectfully.
>
> Each unique value of the elements in this column was assigned a value with the naming scheme - 'cat1-cat9' and 'subcat1-subcat24'. The two new columns(category and subcategory) along with their respective unique values(category_id and subcategory_id) were extracted into new dataframes(category_df and subcategory_df).
>
> New Data Frames were created and saved as a csv file in the 'Output' directory namely - [category.csv](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Output/category.csv) , and [subcategory.csv](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Output/subcategory.csv) .

2. Campaign Dataframe:
> The 'crowdfunding_info_df' dataframe was renamed as 'campaign_df' for simplicity of understanding the code.
>
> The 'blurb' column header was renamed to 'description', 'launched_at' column header was renamed to 'launched_date', and 'deadline' column header was renamed to 'end_date' for a more relevant naming scheme.
>
> The Datatypes for 'goal' and 'pledged' columns were changed from integer datatype to float datatype. The 'launched_date' and 'end_date' columns were changed from integer datatype to datetime objects making the data more relevant for the final database.
>
> Finally the 'campaign_df' dataframe was merged with 'category_df' and subcategory_df' dataframes on the 'category' and 'subcategory' columns respectfully. This new dataframe is called 'campaign_merged_df'
>
> We finally drop the unwanted columns which include - 'staff_pick','spotlight','category & sub-category','category','subcategory' columns.
>
> The final campaign dataframe is named 'campaign_cleaned' and saved as a CSV file in the Output directory called - [campaign.csv](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/Output/campaign.csv)
>

3. Contacts Dataframe:

>convert each row to a dictionary by iterating through the 'contact_info_df' dataframe.
>
> The list of values from this dictionary was added to a new dataframe as seperate columns, and the column header was named according to the 'key' names within the same dictionary.
>
> The 'name' column was split into the 'first_name' and 'second_name' columns
>
>Finally the columns were rearranged to fit the requirements for the database.


### Load:

> We first created a new database by drawing out an ERD diagram on QuickDatabaseDiagrams application as shown below
![ERD diagram(QuickDatabaseDiagram)](https://github.com/DarylPinto26/Crowdfunding_ETL/blob/main/ERD%20image/ERD.png)
>
The following are the datatypes along with their relations for each table as coded into PostgreSQL to create the tables:

1. 'campaign' Table:
> "cf_id" - INTEGER - PRIMARY KEY
> 
> "contact_id" - INTEGER - FOREIGN KEY referencing contacts.contact_id
> 
> "company_name" - STRING
> 
> "description" - STRING
> 
> "goal" - FLOAT
> 
> "pledged" - FLOAT
> 
> "outcome" - STRING
> 
> "backers_count" - STRING
> 
> "country" - STRING
> 
> "currency" - STRING
> 
> "lauched_date" - DATE
> 
> "end_date" - DATE
> 
> "category_id" - STRING - FOREIGN KEY referencing category.category_id
> 
> "subcategory_id" - STRING - FOREIGN KEY referencing subcategory.subcategory_id

2. 'contacts' Table:
>"contact_id" - INTEGER - PRIMARY KEY
>
> "first_name" - STRING
>
> "last_name" - STRING
>
> "email" - STRING

3. 'category' Table:
>"category_id" - STRING - PRIMARY KEY 
>
> "category" - STRING

4. 'subcategory' Table:
>"subcategory_id" - STRING - PRIMARY KEY
>
> "subcategory" - STRING"


The following project was undertaken to understand the intricasies involved in creating an ETL pipeline, and how data must be manipulated in order to fit the requirements of a relational database.
