### DP-203 Azure Data Engineer
1. **[Introduction](#Introduction)**<br>
2. **[Azure Free Account](#Azure-Free-Account)**<br>
3. **[Storage Account](#Storage-Account)**<br>
4. **[Azure Sql Database](#Azure-Sql-Database)**<br>
5. **[Azure Data Factory](#Azure-Data-Factory)**<br>
6. **[Integration runtimes](#Integration-runtimes)**<br>
7. **[Linked Service to blob](#Linked-Service-to-blob)**<br>
8. **[Linked Service to Azure Sql Database](#Linked-Service-to-Azure-Sql-Database)**<br>
9. **[Data Sets](#Data-Sets)**<br>
10. **[Create Pipenine from Blob to Azure Sql Database](#Create-Pipenine-from-Blob-to-Azure-Sql-Database)**<br>
11. **[Additional Columns](#Additional-Columns)**<br>
12. **[Create Pipenine from Blob to Blob](#Create-Pipenine-from-Blob-to-Blob)**<br>
13. **[Install SQL Server](#Install-SQL-Server)**<br>
15. **[Self Hosted IR](#Self-Hosted-IR)**<br>
16. **[Create Pipenine from Blob to MS Sql Server](#Create-Pipenine-from-Blob-to-MS-Sql-Server)**<br>
17. **[Create Pipenine from Azure SQL DB to MS Sql Server DB](#Create-Pipenine-from-Azure-SQL-DB-to-MS-Sql-Server-DB)**<br>


# Introduction
## What is ETL
  - **Extract**: Get Required data(required Tables/Columns/rows) from hetrogenious/homogenious source.
      - Amazon.in > Example of Storage MySQL(OLTP)
      - amazon.co.uk > Example of Storage MS SQL Server(OLTP)
      - amazon.com > Example of Storage PostgresQL(OLTP)
- **Transform**: Convert one form of data into another form (Data Wrangling)
      - Convert one currency(example INR) into another currency(USD)
      - Convert India distance KM terminolgy into USA miles terminology
      - Converting Unix timestamp into windows timestamp
      - Converting all data in a consistency format (1 or M > Male, 0 or F > Female)   
 - **Load**: Final Data which is useful for Analysis/Analytics, will be loadded into warehouse / Datalakes /ADLS /Synposis
## What is ELT ?
- It is same as ETL but the order of work is different
## Different Tools ETL/ELT ?
  - Informatica (ETL/ELT)
  - ODI (ELT)
  - ADF (ETL/ELT)
  - .... etc
## Different BI Tools ?
  - Power BI
  - Tableau
  - ...etc
# Azure Free Account
## Azure Free Account with Credit Card
  - Click on the URL [Azure Free Account]( https://azure.microsoft.com/en-in/free/) > Click on **Start Free** > Provide your emailid > Follow the wizard
## Azure Free Account with Student Mailid
  - Click on the URL [Azure Student Free Account]( https://azure.microsoft.com/en-in/free/students/) > Click on **Start Free** > Provide your emailid > Follow the wizard
## Azure Free sandbox
  - Click on the URL [Azure Free Sandbox](https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/5-exercise-create-a-storage-account?ns-enrollment-type=learningpath&ns-enrollment-id=learn.store-data-in-azure) > In the same page click on **Azure Portal**
  - Note: Few Services only available in the sandbox
# Storage Account
  - Azure Storage is a Microsoft-managed service providing cloud storage that is 
      - highly available
      - secure
      - durable
      - scalable
      - redundant. 
  - Azure Storage includes Azure Blobs (objects), Azure Data Lake Storage Gen2, Azure Files, Azure Queues, and Azure Tables
## Lab
  - Open [Azure Portal](https://portal.azure.com/)> > Click on the search bar > Type **Storage accounts** > Click on **Storage Accounts**
  - Click on **Create** > Under **Basics** tab provide below details
      - Subscription: **rritecsubscription**
      - Resource Group: **rritecresoucegroup**
      - Storage Account Name: **rritecsa**
      - Region: **(US) East US**
      - Performance: **Standard**
      - Redundancy: **Locally-Redundant Storage (LRS)**
  - Click on **Advanced** Tab > select **Enable hierarchical namespace**
  - Click on **Review**
  - Click on **Create**
## Container
  - Click on **Data Lake Storage** > Click on **Container** > Name it as **rriteccontainer** > Click on **Create**
  - ![image](https://user-images.githubusercontent.com/20516321/209080454-923c3672-5e86-4abb-a877-a85f5f43f26d.png)
## Folder
  - Open **rriteccontainer** > Click on **Add Directory** > Name it as **input**
  - Click on **Add Directory** > Name it as **output**
  - ![image](https://user-images.githubusercontent.com/20516321/209080956-412e8fa4-eef5-43f7-86b3-58cbc199ae78.png)
## Upload File
  - Open **rriteccontainer** > open **input** folder > Click on **upload** > from **labdata** select **emp.csv** > Click on **upload**
  - Right Click on **emp.csv** > observe all properties
  - ![image](https://user-images.githubusercontent.com/20516321/209083873-83ee8400-13d9-497a-8772-95e3ff065fa3.png)
# Azure Sql Database
  - Best for modern cloud applications. Hyperscale and serverless
## Lab 1
  - In search box type **Azure SQL** > Under **services** > Click on **Azure SQL**
  - ![image](https://user-images.githubusercontent.com/20516321/209273844-196f7151-7378-40ea-a945-60bb8d8ef89b.png)

  - Click on **Create** > Select **Resource Type** as **Single Database**> Click on **Create** > provide below details accordingly as for your names
      - **Subsription:** Azure For Students
      - **Resource Groups**: master-rritec
      - **Database Name:** rritecazuresqldb
      - **Server:** click on **create new** > **Server Name:** rritecazuresqlserver > **Location:** (US) East US > Select **Use SQL Authentication** 
      - **Server admin login:**: saadmin
      - **password:** RRitec123$
      - **conformpassword:** RRitec123$
      - Click on **ok**
    - **workload environment:** Development
    - **Compute+Storage:** General purpose server less
    - **Backup Storagy Redundancy:** Local Redunt Backup Storage
    - Click on **Networking** tab > select **public Network Access:** Selected Networks
    - Click on **Add your client IPv4 address**
    - select **Allow Azure Services and resources to access this server**    - 
    - Click on **Review + Create**
    - Click on **Create**
    - ![image](https://user-images.githubusercontent.com/20516321/209275635-0512b890-d319-4a1b-b6f2-1eaa7b576eb8.png)

  ## Lab 2: create one table
  - Open **rritecazuresqldb**
  - Click on **Query Editor(preview)**
  - Under **sql server authentication** > provide **username:** as **saadmin** > **password:** as **RRitec123$**
  - Click on **ok**
  - Create emp,dept and salgrade tables and insert some data by running below code
      ``` sql

          CREATE TABLE [dbo].[DEPT]
          (DEPTNO INT PRIMARY KEY ,
          DNAME VARCHAR(20),
          LOC VARCHAR(20) );

          GO

          INSERT INTO [dbo].[DEPT] VALUES (10, 'ACCOUNTING', 'NEW YORK');

          INSERT INTO [dbo].[DEPT] VALUES (20, 'RESEARCH', 'DALLAS');

          INSERT INTO [dbo].[DEPT] VALUES (30, 'SALES', 'CHICAGO');

          INSERT INTO [dbo].[DEPT] VALUES (40, 'OPERATIONS', 'BOSTON');


          CREATE TABLE [dbo].[EMP]
          (EMPNO INT PRIMARY KEY,
          ENAME VARCHAR(20),
          JOB VARCHAR(20),
          MGR INT,
          HIREDATE DATE,
          SAL MONEY,
          COMM MONEY,
          DEPTNO INT );

          GO

          INSERT INTO [dbo].[EMP] VALUES (7369, 'SMITH', 'CLERK', 7902, '17-DEC-1980', 800, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7499, 'ALLEN', 'SALESMAN', 7698, '20-FEB-1981', 1600, 300, 30);

          INSERT INTO [dbo].[EMP] VALUES (7521, 'WARD', 'SALESMAN', 7698, '22-FEB-1981', 1250, 500, 30);

          INSERT INTO [dbo].[EMP] VALUES (7566, 'JONES', 'MANAGER', 7839, '2-APR-1981', 2975, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7654, 'MARTIN', 'SALESMAN', 7698, '28-SEP-1981', 1250, 1400, 30);

          INSERT INTO [dbo].[EMP] VALUES (7698, 'BLAKE', 'MANAGER', 7839, '1-MAY-1981', 2850, NULL, 30);

          INSERT INTO [dbo].[EMP] VALUES (7782, 'CLARK', 'MANAGER', 7839, '9-JUN-1981', 2450, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (7788, 'SCOTT', 'ANALYST', 7566, '09-DEC-1982', 3000, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7839, 'KING', 'PRESIDENT', NULL, '17-NOV-1981', 5000, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (7844, 'TURNER', 'SALESMAN', 7698, '8-SEP-1981', 1500, 0, 30);

          INSERT INTO [dbo].[EMP] VALUES (7876, 'ADAMS', 'CLERK', 7788, '12-JAN-1983', 1100, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7900, 'JAMES', 'CLERK', 7698, '3-DEC-1981', 950, NULL, 30);

          INSERT INTO [dbo].[EMP] VALUES (7902, 'FORD', 'ANALYST', 7566, '3-DEC-1981', 3000, NULL, 20);

          INSERT INTO [dbo].[EMP] VALUES (7934, 'MILLER', 'CLERK', 7782, '23-JAN-1982', 1300, NULL, 10);

          INSERT INTO [dbo].[EMP] VALUES (1234, 'Ram', 'CLERK', 7782, '23-JAN-1982', 1400, NULL, 50);

          GO

          CREATE TABLE [dbo].[SALGRADE]
          (GRADE INT NOT NULL,
          LOSAL MONEY,
          HISAL MONEY );

          GO

          INSERT INTO [dbo].[SALGRADE] VALUES (1, 700, 1200);

          INSERT INTO [dbo].[SALGRADE] VALUES (2, 1201, 1400);

          INSERT INTO [dbo].[SALGRADE] VALUES (3, 1401, 2000);

          INSERT INTO [dbo].[SALGRADE] VALUES (4, 2001, 3000);

          INSERT INTO [dbo].[SALGRADE] VALUES (5, 3001, 9999);
          ```
  - Observe data by runing 
      ``` sql
      select * from emp
      ```
  - ![image](https://user-images.githubusercontent.com/20516321/209278382-d5706988-accb-4f72-add2-5f473a0f774d.png)

## Lab 3: Login and work in SSMS ttol
  - Instal SSMS tool by following [url](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#instal-sql-server-management-studio-ssms)
  - open **rritecAzuresqldb** > copy serbername
  - ![image](https://user-images.githubusercontent.com/20516321/209279155-117ad993-851b-4bb2-b732-956579425adc.png)

  - open SSMS tool
  - Provide below information
  - ![image](https://user-images.githubusercontent.com/20516321/209279299-d777b4cd-38e9-4e52-a832-c592d7c1d8a9.png)

  - Click on **Connect**
  - Expand **Databases**
  - Expand **rritecazuresqldb** > Expend **Tables**
  - Right click on **emp** table > click on **select top 1000 rows**
  - ![image](https://user-images.githubusercontent.com/20516321/209279628-efbc9e45-3ceb-431f-8974-8dfb1d27d141.png)

  - observe **query** and **result**
  - ![image](https://user-images.githubusercontent.com/20516321/209279761-0cdbb8b8-8104-4039-9221-72955c9ea239.png)
## Lab 4(optional): Login and work in Azure Data Studio tool
  - Instal Azure Data Studio and explore your own
# Azure Data Factory
  - In search box type **Data Factories** > Under **services** > Click on **Data Factories**
  - ![image](https://user-images.githubusercontent.com/20516321/209284786-7918e604-260e-479b-9b5d-30813b9ea286.png)

  - Click on **Create**
      - **Subsription:** Azure For Students
      - **Resource Groups**: master-rritec
      - **Name:** rritecadf
      - **Region:**East US
      - **Version:** V2
  - Click on **Review & Create**
  - Click on **Create**
  - ![image](https://user-images.githubusercontent.com/20516321/209289546-3f2a5fb3-8e31-492d-87cf-a9640ac9789a.png)
  - Click on **Go to Resource**
  - Click on **Launch Studio**
  - Observe all options
# Integration runtimes
  - Refer the [doc](https://learn.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)
# Linked Service to blob
  - Linked service defines the connection information to a data store or compute.
## Lab
  - Click on **Manage**
  - Click on **Linked Services**
  - Click on **New**
  - Under **Data Store** > select **Azure Blob Storage** > Click on **Continue**
  - **Name** it as **ls_to_blob_rritecsa**
  - **Connect Via Integration runtime:** AutoResloveIntegrationRuntime
  - **Authentication Type:** Account Key
  - **Account Selection Method:** From Azure Subscription
  - **Azure Subscription:** Azure For Students
  - **Storage Account Name:** rritecsa
  - Click on **Test Connection**
  - ![image](https://user-images.githubusercontent.com/20516321/209294913-03b3d076-39b6-4a3b-8415-104ee14f4ca6.png)
  - Click on **Create** -  
  - 
# Linked Service to Azure Sql Database  
## Lab
  - Click on **Manage**
  - Click on **Linked Services**
  - Click on **New**
  - Under **Data Store** > select **Azure SQL Database** > Click on **Continue**
  - **Name** it as **ls_to_rritecAzureSqlDB**
  - **Connect Via Integration runtime:** AutoResloveIntegrationRuntime
  - **Account Selection Method:** From Azure Subscription
  - **Azure Subscription:** Azure For Students
  - **Server Name:** rritecAzureSqlServer
  - **Database Name:** rritecAzureSqlDB
  - **Authentication Type:** SQL Authentication
  - **username:** saadmin
  - **password:** RRitec123$
  - Click on **Test Connection**  
  - ![image](https://user-images.githubusercontent.com/20516321/209418103-69375600-171e-47db-9c1f-3bb7fbff9199.png)

  - Click on **Create**

# Data Sets
  - Click on **Author**
  - Right Click on datasets > Create new **Folder** > Name it as **Source**
  - Right Click on **Source** folder > Click on **New Dataset** > Provide below options
  - ![image](https://user-images.githubusercontent.com/20516321/209418572-7638b228-3ec1-4ffd-ae70-af22b80cad39.png)
  - Right Click on datasets > Create new **Folder** > Name it as **target**
  - Right Click on **target** folder > Click on **New Dataset** > Provide below options
  - ![image](https://user-images.githubusercontent.com/20516321/209418743-bcf5f118-00b6-442b-bb0e-5cecbc75b36c.png)

# Create Pipenine from Blob to Azure Sql Database
  - Click on **Author**
  - Right Click on **pipelines** > Click on **New Folder** > Name it as **rritec_pipelines**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p01_from Blob to Azure Sql Database**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **Genera** tab > name it as **Copy_from_blob_to_AzureSqlDB**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_emp** > Select **Table Option** as **Auto Create Table**
  - Click on **Debug**
  - Under **output** tab > Observe run **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209774609-19490338-3be6-4f65-8a4e-bc762b3a7dc0.png)

  - Click on **publish** to save the work
  - ![image](https://user-images.githubusercontent.com/20516321/209419233-cd322af4-fb3e-4b62-9713-228462d1bbe8.png)
  - Understand the **output JSON** of **copy Activity**. For More information refer [URL](https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-monitoring?tabs=data-factory#monitor-programmatically) 
  - open SSMS > observe data in table
  - ![image](https://user-images.githubusercontent.com/20516321/209419293-07193ab6-aa37-49d6-bd60-ef786cbcc0ab.png)

# Additional Columns
  - Open Pipeline **p01_from Blob to Azure Sql Database**
  - Select **Copy Data** Activity
  - Click on **Source** tab 
  - In **Additional Columns**  > Click on **New**
  - provide as shown below
  - ![image](https://user-images.githubusercontent.com/20516321/209504074-83671970-e0cd-4a35-a09e-73a7b2e85ec6.png)

  - Click on **Sink** tab
  - In **Pre Copy Script** > type below sql code
``` sql
drop table [dbo].[TGT_EMP]
```
  - ![image](https://user-images.githubusercontent.com/20516321/209504332-94e596eb-5636-4627-b45a-b06c12efb274.png)

  - Click on **debug**
  - observe output jsons
  - open SSMS > observe data in table

# Create Pipenine from Blob to Blob
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p02_from Blob to Blob**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_blob_to_Blob**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_emp1**
  - ![image](https://user-images.githubusercontent.com/20516321/209508743-32207e73-d66b-4ec4-a705-fe271ef6f839.png)

  - Click on **Debug**
  - Under **Output** > observe **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209774847-4c1331d1-837d-4ff9-952f-33ec90b94657.png)
 

# Install SQL Server
  - Follow the [doc](https://github.com/rritec/powerbi/blob/master/Notebooks/PBI_01_01_Introduction_Installation.md#msft-sql-server-installation) and install SQL Serer database

# Self Hosted IR
  - Perform data flows, data movement and dispatch activities to **external compute**
  - In **ADF** > Clcik on **Manage** > Under **Connections** > Click on **Integration Runtimes**
  - Click on **New**
  - Click on **Azure, Self-Hosted**
  - Click on **Self-Hosted**
  - Name it as **Self-Hosted-IR**
  - Click on **Create**
  - Click on **Express Setup** and install the software

# Create Pipenine from Blob to MS Sql Server
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p03_from Blob to MS Sql Server**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_blob_to_MS_SQL_Server**
  - Click on **Source** tab > Select **Source Dataset** as **src_emp**
  - Click on **Sink** tab > Select **Sink dataset** as **tgt_sql_server_emp**
  - Click on **Debug**
  - Under **Output** > observe **Details**
  - ![image](https://user-images.githubusercontent.com/20516321/209775129-191c309d-ccce-4c27-9c82-6aad1e5228fa.png)


# Create Pipenine from Azure SQL DB to MS Sql Server DB
  - Click on **Author**
  - Right click on **rritec_pipelines** folder > Click on **New Pipeline** > Name it as **p04_from Azure SQL DB to MS Sql Server DB**
  - Under **Activities** > Expand **Move & Transform** > Drag and drop **Copy Data** activity
  - Under **General** tab > name it as **Copy_from_Azure_sql_DB_to_MS_SQL_Server_DB**
  - Click on **Source** > Click on **New** > Select **Azure SQL Database** > Name it as **src_ds_azure_sql_emp**
  - Select **Linked Service** as **ls_to_rritecAzureSQlDB** > Select **table name** as **dbo.EMP**
  - Clcik on **OK**
  - Under **additional Columns** > click on **New** > **Name** it as **LoadDate** > **Value** as **@pipeline().TriggerTime**
  - ![image](https://user-images.githubusercontent.com/20516321/209767367-0c181c7d-7161-4670-832f-a655120f414a.png)

  - Click on **Sink** > Click on **New**
  - Select **SQL Server** > Click on **Continue**
  - **Name** it as **tgt_ds_sql_server_temp**
  - Select **Linked Service** as **ls_ms_sql_server**
  - provide **Schema** as **dbo** > **table** as **temp** > **Import Schema** as **None** > Click on **OK**
  - Select **Table Option** as **Auto Create Table**
  - ![image](https://user-images.githubusercontent.com/20516321/209773977-b189c318-fa71-4801-9230-b4021515b052.png)

  
  - Click on **Debug**
  - Observe Output.
  - ![image](https://user-images.githubusercontent.com/20516321/209774340-24d92c19-3170-41c9-a362-c46240eadee3.png)








