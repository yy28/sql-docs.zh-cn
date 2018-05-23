---
title: PolyBase 入门 | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: database
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
caps.latest.revision: 78
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfde818a22771ba7bfa08259e3a34eff68fb1aea
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="get-started-with-polybase"></a>PolyBase 入门
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题包含针对 SQL Server 实例运行 PolyBase 的相关基础知识。
  
 运行下面的步骤之后，你将：  
  
-   安装 PolyBase 并可在你的服务器上运行  
  
-   获得用于创建 PolyBase 对象的语句示例  
  
-   了解如何在 SQL Server Management Studio (SSMS) 中管理 PolyBase 对象  
  
-   获得使用 PolyBase 对象的查询示例    

## <a name="install-polybase"></a>安装 PolyBase  
如果尚未安装 PolyBase，请参阅 [PolyBase 安装](../../relational-databases/polybase/polybase-installation.md)。 这篇安装文章介绍了安装的先决条件。
  
### <a name="how-to-confirm-installation"></a>如何确认安装  
 安装完成后，运行以下命令以确认已成功安装 PolyBase。 如果已安装 PolyBase，则返回 1；否则返回 0。  
  
```sql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> 配置 PolyBase  
 安装后，必须配置 SQL Server 以使用 Hadoop 版本或 Azure Blob 存储。 PolyBase 支持两个 Hadoop 提供程序：Hortonworks 数据平台 (HDP) 和 Cloudera 分布式 Hadoop (CDH)。  支持的外部数据源包括：  
  
-   Linux/Windows Server 上的 Hortonworks HDP 1.3  
  
-   Linux 上的 Hortonworks HDP 2.1 - 2.6

-   Windows Server 上的 Hortonworks HDP 2.1 - 2.3  
  
-   Linux 上的 Cloudera CDH 4.3  
  
-   Linux 上的 Cloudera CDH 5.1 – 5.5、5.9 - 5.13  
  
-   Azure Blob 存储  
 
Hadoop 遵循其新版本的“Major.Minor.Version”模式。 支持的主要和次要版本中的所有版本均受支持。
 

>  [!NOTE]
> Azure Data Lake Store 连接仅在 Azure SQL 数据仓库中受支持。
  
### <a name="external-data-source-configuration"></a>外部数据源配置  
  
1.  运行 [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ‘hadoop connectivity’ 并设置适当的值。 默认情况下，hadoop 连接设置为 7。 若要查找值，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
      ```sql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  必须使用 **services.msc**重启 SQL Server。 重启 SQL Server 会重启这些服务：  
  
    -   SQL Server PolyBase 数据移动服务  
  
    -   SQL Server PolyBase 引擎  
  
 ![在 services.msc 中停止和启动 PolyBase 服务](../../relational-databases/polybase/media/polybase-stop-start.png "在 services.msc 中停止和启动 PolyBase 服务")  
  
### <a name="pushdown-configuration"></a>下推配置  
 若要提高查询性能，请对 Hadoop 群集启用下推计算：  
  
1.  在 SQL Server 的安装路径中查找文件 **yarn-site.xml** 。 通常情况下，该路径为：  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  对于 Hadoop 计算机，在 Hadoop 配置目录中查找类似文件。 在文件中，查找并复制配置密钥 yarn.application.classpath 的值。  
  
3.  对于 SQL Server 计算机，在 **yarn.site.xml 文件中，** 查找 **yarn.application.classpath** 属性。 将 Hadoop 计算机的值粘贴到值元素中。  
  
4. 对于所有 CDH 5.X 版本，你都需要将 mapreduce.application.classpath 配置参数添加到 yarn.site.xml 文件的末尾或添加到 mapred-site.xml 文件中。 HortonWorks 在 yarn.application.classpath 配置中包括了这些配置。 有关示例，请参阅 [PolyBase 配置](../../relational-databases/polybase/polybase-configuration.md)。

 
## <a name="scale-out-polybase"></a>横向扩展 PolyBase  
 PolyBase 组功能允许你创建 SQL Server 实例的群集来处理来自外部数据源的大型数据集，从而通过一种扩展的方式提高查询性能。  
  
1.  在多台机器上安装具有 PolyBase 的 SQL Server。  
  
2.  选择一个 SQL Server 作为头节点。  
  
3.  通过运行 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)添加作为计算节点的其它实例。  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  在计算节点上重启 PolyBase 数据移动服务。  
  
 有关详细信息，请参阅 [PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
  
## <a name="create-t-sql-objects"></a>创建 T-SQL 对象  
 根据外部数据源（Hadoop 或 Azure 存储）创建对象。  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).    
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
-- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = MyHadoopCluster,  
        FILE_FORMAT = TextFileFormat  
);  
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Azure Blob 存储  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH (  
       FORMAT_TYPE = DELIMITEDTEXT,   
       FORMAT_OPTIONS (
         FIELD_TERMINATOR ='|',   
         USE_TYPE_DEFAULT = TRUE
       )
);
         
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
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
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>PolyBase Queries  
 PolyBase 适用于三个函数：  
  
-   对外部表的即席查询。  
  
-   导入数据。  
  
-   导出数据。  
  
### <a name="query-examples"></a>查询示例  
  
-   即席查询  
  
    ```sql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   导入数据  
  
    ```sql  
    -- PolyBase Scenario 2: Import external data into SQL Server.  
    -- Import data for fast drivers into SQL Server to do more in-depth analysis and  
    -- leverage Columnstore technology.  
  
    SELECT DISTINCT   
            Insured_Customers.FirstName, Insured_Customers.LastName,   
            Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
    INTO Fast_Customers from Insured_Customers INNER JOIN   
    (  
            SELECT * FROM CarSensor_Data where Speed > 35   
    ) AS SensorD  
    ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
    ORDER BY YearlyIncome  
  
    CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
    ```  
  
-   导出数据  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
    reconfigure  
  
    -- Create an external table.   
    CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
            [FirstName] char(25) NOT NULL,   
            [LastName] char(25) NOT NULL,   
            [YearlyIncome] float NULL,   
            [MaritalStatus] char(1) NOT NULL  
    )  
    WITH (  
            LOCATION='/old_data/2009/customerdata',  
            DATA_SOURCE = HadoopHDP2,  
            FILE_FORMAT = TextFileFormat,  
            REJECT_TYPE = VALUE,  
            REJECT_VALUE = 0  
    );  
  
    -- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
    INSERT INTO dbo.FastCustomer2009  
    SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
    ON (T1.CustomerKey = T2.CustomerKey)  
    WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
    ```  
  
## <a name="managing-polybase-objects-in-ssms"></a>在 SSMS 中管理 PolyBase 对象  
 在 SSMS 中，外部表在单独的文件夹“外部表” 中显示。 外部数据源和外部文件格式位于“外部资源” 下的子文件夹中。  
  
 ![SSMS 中的 PolyBase 对象](../../relational-databases/polybase/media/polybase-management.png "SSMS 中的 PolyBase 对象")  
  
## <a name="troubleshooting"></a>故障排除  
 使用 DMV 来进行性能和查询故障排除。 有关详细信息，请参阅 [PolyBase 故障排除](../../relational-databases/polybase/polybase-troubleshooting.md)。  
  
 从 SQL Server 2016 RC1 升级到 RC2 或 RC3 之后，查询可能会失败。 有关详细信息和补救措施，请参阅 [SQL Server 2016 发行说明](../../sql-server/sql-server-2016-release-notes.md) 并搜索“PolyBase”。  
  
## <a name="next-steps"></a>后续步骤  
 若要了解横向扩展功能，请参阅 [PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)。  若要监视 PolyBase，请参阅 [PolyBase 故障排除](../../relational-databases/polybase/polybase-troubleshooting.md)。 若要对 PolyBase 性能进行故障排除，请参阅[使用动态管理视图对 PolyBase 进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)。  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase 横向扩展组](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [PolyBase 存储过程](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
