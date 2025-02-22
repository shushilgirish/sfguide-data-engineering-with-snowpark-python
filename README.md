# Data Engineering Pipelines with Snowpark Python

This repository contains the code for the *Data Engineering Pipelines with Snowpark Python* Snowflake Quickstart.

### ➡️ For overview, prerequisites, and to learn more, complete this end-to-end tutorial [Data Engineering Pipelines with Snowpark Python](https://quickstarts.snowflake.com/guide/data_engineering_pipelines_with_snowpark_python/index.html?index=..%2F..index#0) on quickstarts.snowflake.com.

---

## Overview

Here is an overview of what we'll build in this lab:

<img src="images/demo_overview.png" width=800px>

Below are the screenshots of every step taken to build and orchestrate tasks in Snowflake:

### Step 0: Snowflake Data Pipeline GitHub Repository

<img width="1278" alt="image" src="https://github.com/user-attachments/assets/29920049-0c9a-4e0c-9089-19ff7a89ca90" />

### Step 1: Fork Repository and Run Codespace

- Fork the repository and run your codespace in your forked repository.
- It will take some time to load the container, Anaconda, and VS Code setup files.
- Once done, it should appear like this:
  
  ![image](https://github.com/user-attachments/assets/dd6e3951-4939-4f8d-8643-2dd7aed81d6e)
  
- Ensure Anaconda is installed.

### Step 2: Connect Snowflake Credentials

- Connect your Snowflake credentials to the Snowflake extensions.
  
  ![image](https://github.com/user-attachments/assets/27f141e6-1653-4dd9-a2e4-f536a4c35e50)
  
- Provide the user, account, and password in the `connections.toml` file in the Snowflake directory.

### Step 3: Get Frostbyte Data and Create Schemas

- After successfully connecting with Snowflake, get the `frostbyte_data_LLC` from the shared place in the **DataProduct** section of the Snowflake account.
- Create schemas and stage the Frostbyte data to the `EXTERNAL` schema.
- Create the necessary UDFs.
  
  ![image](https://github.com/user-attachments/assets/bfd90930-48a6-47e7-8962-9a405f6dbeb5)

### Step 4: Load Raw Data from AWS Stage

- Load the raw data from AWS stage.
- Get all corresponding tables into the schemas: `RAW_POS` and `RAW_CUSTOMER`.

#### Table Structure:

**POS_TABLES:**
```python
['country', 'franchise', 'location', 'menu', 'truck', 'order_header', 'order_detail']
```

**CUSTOMER_TABLES:**
```python
['customer_loyalty']
```

**Table Dictionary:**
```python
TABLE_DICT = {
    "pos": {"schema": "RAW_POS", "tables": POS_TABLES},
    "customer": {"schema": "RAW_CUSTOMER", "tables": CUSTOMER_TABLES}
}
```

- Create a view called `pos_flattend_v` combining all the tables from `RAW_POS` schema.
- Create a stream for the view `pos_flattened_v_stream` in the **harmonized** schema.

### Step 5: Create UDF for Temperature Conversion

- Define a UDF function `fahrenheit_to_celsius` to convert temperature units.
- Use **scipy** for conversion and update `requirements.snowflake.txt`.
  
  ![image](https://github.com/user-attachments/assets/a3ea0830-cd6b-4f97-9025-f18d8c039587)

### Step 6: Create Stored Procedure `orders_update_sp`

- This procedure creates the `orders` table, capturing new records added into `pos_flattened_v_stream`.

### Step 7: Create Stored Procedure `daily_city_metrics_update_sp`

- This procedure merges weather data into the `orders` table.
- This stored procedure should run **after** `orders_update_sp`.

### Step 8: Orchestrate Jobs Using Snowflake Tasks

- Create two tasks for running the stored procedures.

### Step 9: Execute Tasks Manually

- Run the SQL query manually since scheduling is not added.
- The task gets skipped initially due to no new data in `pos_flattened_v_stream`.
- Load **2022 data** into the table.
- Execute the task again.

### Step 10: Observe Task Execution

- After running the task again, check the execution status.
  
  ![image](https://github.com/user-attachments/assets/9153df8e-2d24-4f0c-a4c3-41ceb742349c)

- Below is the workflow of the task in Snowflake:
  
  ![image](https://github.com/user-attachments/assets/08ac02cd-7b75-4559-808f-9b3b0cb5093e)

### Step 11: Deploy Data Pipeline Using GitHub Actions

- Add your **secrets** in your repository.
  
  ![image](https://github.com/user-attachments/assets/117a4ac0-88b6-4518-81fd-43ff96e9b457)

- Manually trigger the deployment from the **Actions** section.
  
  ![image](https://github.com/user-attachments/assets/3995959d-ff5f-4bd9-a13a-4f1f85ab7e87)

---

This guide provides a complete walkthrough of building and orchestrating Snowflake tasks using Snowpark Python.

