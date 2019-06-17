---
title: 配置 PolyBase 以访问 Hadoop 中的外部数据 | Microsoft Docs
description: 介绍如何在并行数据仓库，若要将连接到外部 Hadoop 配置 PolyBase。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: afa5728d651444aeb633c69b310c36af6b0e821a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175262"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>配置 PolyBase 以访问 Hadoop 中的外部数据

本文介绍如何在 Hadoop 中的查询外部数据的 APS 设备上使用 PolyBase。

## <a name="prerequisites"></a>先决条件

PolyBase 支持两个 Hadoop 提供程序：Hortonworks 数据平台 (HDP) 和 Cloudera 分布式 Hadoop (CDH)。 Hadoop 遵循其新版本的“Major.Minor.Version”模式，且主要和次要版本中支持的所有版本均受支持。 支持以下 Hadoop 提供程序：
 - Linux/Windows Server 上的 Hortonworks HDP 1.3  
 - Linux 上的 Hortonworks HDP 2.1-2.6
 - Linux 上的 Hortonworks HDP 3.0 3.1
 - Windows Server 上的 Hortonworks HDP 2.1 - 2.3  
 - Linux 上的 Cloudera CDH 4.3  
 - Cloudera CDH 5.1-5.5、 5.9-5.13 Linux 上

### <a name="configure-hadoop-connectivity"></a>配置 Hadoop 连接

首先，配置 AP 以使用特定的 Hadoop 提供程序。

1. 使用“hadoop connectivity”运行 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 并为提供程序设置适当的值。 若要为提供程序查找值，请参阅 [PolyBase 连接配置](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 and 3.0 - 3.1 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 重新启动 APS 区域上，使用服务状态页[设备配置管理器](launch-the-configuration-manager.md)。
  
## <a id="pushdown"></a> 启用下推计算  

若要提高查询性能，请对 Hadoop 群集启用下推计算：  
  
1. 打开远程桌面连接到 PDW 控制节点。

2. 找到文件**yarn-site.xml**在控制节点上。 通常情况下，该路径为：  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. 对于 Hadoop 计算机，在 Hadoop 配置目录中查找类似文件。 在文件中，查找并复制配置密钥 yarn.application.classpath 的值。  
  
4. 在控制节点上，在**yarn.site.xml 文件**查找**yarn.application.classpath**属性。 将 Hadoop 计算机的值粘贴到值元素中。  
  
5. 对于所有 CDH 5.X 版本，你都需要将 mapreduce.application.classpath 配置参数添加到 yarn.site.xml 文件的末尾或添加到 mapred-site.xml 文件中。 HortonWorks 在 yarn.application.classpath 配置中包括了这些配置。 有关示例，请参阅 [PolyBase 配置](../relational-databases/polybase/polybase-configuration.md)。

## <a name="example-xml-files-for-cdh-5x-cluster-default-values"></a>示例 XML 文件 CDH 5.X 群集的默认值

包含 yarn.application.classpath 和 mapreduce.application.classpath 配置的 Yarn-site.xml。

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

如果您选择两个配置设置分解为 mapred-site.xml 和 yarn-site.xml，则文件将如下所示：

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

**mapred-site.xml**

注意，我们添加了属性 mapreduce.application.classpath。 在 CDH 5.x 中，你将在 Ambari 中查找相同的命名约定的配置值。

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
   <property>
     <name>mapred.min.split.size</name>
       <value>1073741824</value>
   </property>
   <property>
     <name>mapreduce.app-submission.cross-platform</name>
     <value>true</value>
   </property>
<property>
     <name>mapreduce.application.classpath</name>
     <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
   </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
     <name>mapreduce.jobhistory.principal</name>
     <value></value>
   </property>
   <property>
     <name>mapreduce.jobhistory.address</name>
     <value></value>
   </property>
-->
</configuration>
```

## <a name="example-xml-files-for-hdp-3x-cluster-default-values"></a>示例 XML 文件 HDP 3.X 群集默认值

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CONF_DIR,/usr/hdp/3.1.0.0-78/hadoop/*,/usr/hdp/3.1.0.0-78/hadoop/lib/*,/usr/hdp/current/hadoop-hdfs-client/*,/usr/hdp/current/hadoop-hdfs-client/lib/*,/usr/hdp/current/hadoop-yarn-client/*,/usr/hdp/current/hadoop-yarn-client/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/lib/*,/usr/hdp/share/hadoop/common/*,/usr/hdp/share/hadoop/common/lib/*,/usr/hdp/share/hadoop/tools/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

## <a name="configure-an-external-table"></a>配置外部表

若要查询 Hadoop 数据源中的数据，必须定义外部表以在 Transact-SQL 查询中使用。 以下步骤介绍如何配置外部表。

1. 在数据库上创建主密钥。 需要加密的凭据机密。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. 为受 Kerberos 保护的 Hadoop 群集创建数据库范围凭据。

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. 使用 [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) 创建外部数据源。

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

4. 使用 [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) 创建外部文件格式。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. 使用 [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md) 创建指向存储在 Hadoop 中的数据的外部表。 在此示例中，外部数据包含汽车传感器数据。

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
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. 在外部表上创建统计信息。

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

下面的即席查询联接关系与 Hadoop 数据。 它将选择快 35 mph，联接结构化的客户数据存储在 AP 中使用存储在 Hadoop 中的汽车传感器数据驱动器的客户。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
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

以下查询将数据从 APS 导出到 Hadoop。 它可用于关系数据存档到 Hadoop 时仍将能够对其进行查询。

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
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

有关 Hadoop 安全设置，请参阅[配置的 Hadoop 安全性](polybase-configure-hadoop-security.md)。<br>
有关 PolyBase 的详细信息，请参阅[什么是 PolyBase？](../relational-databases/polybase/polybase-guide.md)。 
 
