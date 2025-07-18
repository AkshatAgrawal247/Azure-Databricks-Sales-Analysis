# End-to-End Sales Data Analysis in Azure Databricks

This project demonstrates a complete, end-to-end data engineering pipeline built on the Microsoft Azure platform. The primary goal is to ingest raw sales data from a data lake, process and analyze it to derive business insights, and store the results in a reliable and optimized format.

## Objective
To load transaction data from CSV files stored in Azure Data Lake Storage (ADLS) Gen2, join it with product information, perform analysis to extract key business insights, and store the aggregated results in a managed Delta table for reporting and further analysis.

---

## Architecture & Tools
The following technologies were used to build this pipeline:

*   **Cloud Platform:** Microsoft Azure
*   **Data Storage:** Azure Data Lake Storage (ADLS) Gen2
*   **Data Processing:** Azure Databricks
*   **Core Technologies:** Apache Spark, Delta Lake, Python (PySpark)
*   **Authentication:** Azure Active Directory (Microsoft Entra ID) Service Principal

![Architecture Diagram](https://i.imgur.com/nJlL3g0.png)

---

## Methodology

The project was executed in a Databricks Notebook (`Project-Analysis.html`) and followed these key steps:

1.  **Secure Configuration:** A Service Principal was created in Azure AD to provide the Databricks cluster with secure, role-based access to the ADLS Gen2 storage account. The "Storage Blob Data Contributor" role was assigned to ensure appropriate permissions.

2.  **Data Loading (ETL - Extract):** Raw transaction and product data from CSV files stored in ADLS Gen2 were loaded into Spark DataFrames. Schemas were explicitly defined to ensure data integrity and prevent errors.

3.  **Data Transformation & Analysis (ETL - Transform):**
    *   The transaction and product DataFrames were joined on `product_id` to create a unified view.
    *   Key business metrics were calculated using Spark's built-in functions, including:
        *   Average Order Value per customer.
        *   Total spend per customer.
        *   Most popular products sold by quantity.
        *   Top-selling product categories.

4.  **Data Storage (ETL - Load):** The final, enriched DataFrame containing the insights was saved as a managed Delta table in Databricks. Using the Delta Lake format provides ACID transactions, time travel (data versioning), and significantly improves query performance.

5.  **Optimization & Quality:**
    *   The Delta table was optimized using the `OPTIMIZE` and `ZORDER BY` commands to compact small files and co-locate related data, speeding up future queries.
    *   A data quality check was performed on the initial raw data to ensure there were no null values in critical columns.

---

## How to View the Project

The complete code, along with all outputs and visualizations, can be viewed in the **[Project-Analysis.html](Project-Analysis.html)** file included in this repository.

The raw data used for this analysis is available in the `/sample_data` directory.
