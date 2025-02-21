# Data Engineering Pipelines with Snowpark Python
This repository contains the code for the *Data Engineering Pipelines with Snowpark Python* Snowflake Quickstart.

### ➡️ For overview, prerequisites, and to learn more, complete this end-to-end tutorial [Data Engineering Pipelines with Snowpark Python](https://quickstarts.snowflake.com/guide/data_engineering_pipelines_with_snowpark_python/index.html?index=..%2F..index#0) on quickstarts.snowflake.com.

___
Here is an overview of what we'll build in this lab:

<img src="images/demo_overview.png" width=800px>

below are the screenshots of every steps taken to build and orchestrate tasks in snowflake:
0.The snowflake data pipeline github repo:
<img width="1278" alt="image" src="https://github.com/user-attachments/assets/29920049-0c9a-4e0c-9089-19ff7a89ca90" />

1.Fork repository and run your codespace in your forked repository ,
it will take some time to load , your container , anaconda and vscode setup files. Once thats done , you will be displayed like this 
![image](https://github.com/user-attachments/assets/dd6e3951-4939-4f8d-8643-2dd7aed81d6e)
make sure your anaconda is installed.
2.Connect your Snowflake credentials to the snowflake exetensions.
![image](https://github.com/user-attachments/assets/27f141e6-1653-4dd9-a2e4-f536a4c35e50)
give the user,account and password in the connections.toml of the snowflake directory.
3.After successfully connecting with snowflake ,get the frostbyte data :LLC from the sharedplace in the DataProduct section of the Snowflake account.After that create schemas,stage the frostbyte data to the  EXTERNAL schema and create the udf.Below ,I have attached the screenshot of the snowflake queries for this part.
![image](https://github.com/user-attachments/assets/bfd90930-48a6-47e7-8962-9a405f6dbeb5)
4.Load the raw data from the aws stage. Get all the corresponding tables into the schemas: raw_pos and raw_customer.
POS_TABLES = ['country', 'franchise', 'location', 'menu', 'truck', 'order_header', 'order_detail']
CUSTOMER_TABLES = ['customer_loyalty']
TABLE_DICT = {
    "pos": {"schema": "RAW_POS", "tables": POS_TABLES},
    "customer": {"schema": "RAW_CUSTOMER", "tables": CUSTOMER_TABLES}
}
below are the tables for these 2 schemas.
Also create a view called pos_flattend_v combining all the tables from the raw_pos schema and finally create a stream for the view pos_flattened_v_stream in the harmonized schema.
5. Then create an UDF function fahrenheit_to_celsius for converting temperature unit. Later on, we will be using the scipy tool for the conversion and update the tool in the requirements.snowflake.txt 
![image](https://github.com/user-attachments/assets/a3ea0830-cd6b-4f97-9025-f18d8c039587)
6. Create the stored procedure orders_update_sp for creating table orders which captures new records added into the pos_flattened_v_stream 
7. Create another stored procedure daily_city_metrics_update_sp for merging the weather data into the orders table.This store procedure should be executed after successful completion of orders_update_sp().
8. Orchestrate jobs using the snowflake inbuilt tasks .create 2 tasks each for running the stored procedures. 
9.Run the sql query in the step 09 , where you manually excute the tasks as scheduling has not been added.When you run the file , task get skipped as there is no new data in the pos_flattened_v_stream . So we load the 2022 data into the table , and then again start executing the task. 
10. Once you run again after loading the new data, you get to see the tasks running in the screenshot attached below.
![image](https://github.com/user-attachments/assets/9153df8e-2d24-4f0c-a4c3-41ceb742349c)
I have attached the workflow of the task in the snowflake 
![image](https://github.com/user-attachments/assets/08ac02cd-7b75-4559-808f-9b3b0cb5093e)
11. Finally, you have to deploy your data pipeline using the github actions . Before that , add your secrets in your repo like this.
![image](https://github.com/user-attachments/assets/117a4ac0-88b6-4518-81fd-43ff96e9b457)
After that , run the deployment manually in the actions section of the repository.You get to use like this ,
![image](https://github.com/user-attachments/assets/3995959d-ff5f-4bd9-a13a-4f1f85ab7e87)



