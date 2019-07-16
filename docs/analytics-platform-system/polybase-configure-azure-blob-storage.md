---
title: 配置 PolyBase 以访问 Azure Blob 存储中的外部数据 |Microsoft Docs
description: 介绍如何在并行数据仓库，若要将连接到外部 Hadoop 配置 PolyBase。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82c57ef57a01cabf2786c71fc53aed3660289451
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960281"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>配置 PolyBase 以访问 Azure Blob 存储中的外部数据

本文介绍如何使用 PolyBase 来查询 Azure Blob 存储中的外部数据的 SQL Server 实例上。

> [!NOTE]
> APS 目前仅支持本地冗余 (LRS) Azure Blob 存储的标准常规用途 v1。

## <a name="prerequisites"></a>先决条件

 - 在订阅中的 azure Blob 存储。
 - 在 Azure Blob 存储中创建一个容器。

### <a name="configure-azure-blob-storage-connectivity"></a>配置 Azure Blob 存储连接

首先，配置 AP 以使用 Azure Blob 存储。

1. 运行[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 'hadoop connectivity' 设置为 Azure Blob 存储提供程序使用。 若要查找提供程序的值，请参阅 [PolyBase 连接配置](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 重新启动 APS 区域上，使用服务状态页[设备配置管理器](launch-the-configuration-manager.md)。
  
## <a name="configure-an-external-table"></a>配置外部表

若要查询 Azure Blob 存储中的数据，必须定义外部表在 TRANSACT-SQL 查询中使用。 以下步骤介绍如何配置外部表。

1. 在数据库上创建主密钥。 需要加密的凭据机密。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. 创建 Azure Blob 存储的数据库范围凭据。

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) 创建外部数据源。

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. 使用 [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) 创建外部文件格式。

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. 使用 [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md) 创建指向 Azure 存储中存储的数据的外部表。 在此示例中，外部数据包含汽车传感器数据。

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = AzureStorage,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

1. 在外部表上创建统计信息。

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase Queries

PolyBase 适用于三个函数：  
  
- 针对外部表的即席查询。  
- 导入数据。  
- 导出数据。  

下面的查询提供了虚构汽车传感器数据示例。

### <a name="ad-hoc-queries"></a>即席查询  

以下即席查询联接关系数据与在 Azure Blob 存储中。 它将选择快 35 mph，联接结构化的客户数据存储在 SQL Server 中使用 Azure Blob 存储中存储的汽车传感器数据驱动器的客户。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>导入数据  

下面的查询外部数据导入 APS。 此示例数据快速驱动程序导入 APS 进行更加深入的分析。 若要提高性能，它利用 AP 中的列存储技术。  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>导出数据  

以下查询将从 AP 数据导出到 Azure Blob 存储。 它可用于关系数据存档到 Azure Blob 存储，同时仍能对其进行查询。

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>在 SSDT 中查看 PolyBase 对象  

在 SQL Server Data Tools，可以在单独的文件夹中显示外部表**外部表**。 外部数据源和外部文件格式位于“外部资源”  下的子文件夹中。  
  
![在 SSDT 中的 PolyBase 对象](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>后续步骤

有关 PolyBase 的详细信息，请参阅[什么是 PolyBase？](../relational-databases/polybase/polybase-guide.md)。 

