---
title: 将 Spark 连接到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何使用适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器读取和写入 SQL Server。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 3cb36c4bdddfaa97b9b6c08015308799d54cb0dc
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438069"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>如何使用适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器从 Spark 读取和写入 SQL Server

Spark 中的大容量数据处理是一种关键大数据使用模式，之后会将数据写入 SQL Server 以访问业务线应用程序。 这些使用模式受益于使用关键 SQL 优化并提供高效写入机制的连接器。

本文概述了适用于 SQL Server 和 Azure SQL 接口的 Apache Spark 连接器，并将其实例化以用于非 AD 模式和 AD 模式。 然后，提供一个示例，说明如何使用适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器读取和写入大数据群集中的以下位置：
1. SQL Server 主实例
1. SQL Server 数据池

   ![适用于 SQL Server 和 Azure SQL 关系图的 Apache Spark 连接器](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-interface"></a>适用于 SQL Server 和 Azure SQL 接口的 Apache Spark 连接器

SQL Server 2019 为大数据群集提供了[适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器](https://github.com/microsoft/sql-spark-connector)，这些大数据群集使用 SQL Server 批量写入 API 执行 Spark 到 SQL 的写入操作。 适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器基于 Spark 数据源 API，并提供了熟悉的 Spark JDBC 连接器接口。 有关接口参数，请参阅 [Apache Spark 文档](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器由名称 com.microsoft.sqlserver.jdbc.spark 引用。 适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器支持两种与 SQL Server 连接的安全模式（非 Active Directory 模式和 Active Directory (AD) 模式）：
### <a name="non-ad-mode"></a>非 AD 模式：
在非 AD 模式安全性中，每个用户都有一个用户名和密码，在连接器实例化期间需要将它们作为参数提供，以执行读取和/或写入。
以下为非 AD 模式的连接器实例化示例：
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```
### <a name="ad-mode"></a>AD 模式：
在 AD 模式安全性中，用户生成一个 keytab 文件后，需要在连接器实例化期间提供 `principal` 和 `keytab` 作为参数。

在此模式下，驱动程序将 keytab 文件加载到相应的执行器容器。 然后，执行器使用主体名称和 keytab 生成一个令牌，该令牌可用于创建用于读取/写入的 JDBC 连接器。

以下为 AD 模式的连接器实例化示例：
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

下表介绍已更改或新增的接口参数：

| 属性名称 | 可选 | 说明 |
|---|---|---|
| **isolationlevel** | 是 | 此参数描述连接的隔离级别。 连接器的默认值为 READ_COMMITTED |

连接器使用 SQL Server 批量写入 API。 任何批量写入参数都可由用户作为可选参数进行传递，并可由连接器按原样传递到基础 API。 有关批量写入操作的详细信息，请参阅 [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-sample"></a>适用于 SQL Server 和 Azure SQL 示例的 Apache Spark 连接器
本示例执行以下任务：

- 从 HDFS 读取文件并进行一些基本处理。
- 将数据帧作为 SQL 表写入 SQL Server 主实例，然后将表读取到数据帧。
- 将数据帧作为 SQL 外部表写入 SQL Server 数据池，然后将外部表读取到数据帧。
### <a name="prerequisites"></a>先决条件

- [SQL Server 大数据群集](deploy-get-started.md)。

- [Azure Data Studio](https://aka.ms/getazuredatastudio)。

### <a name="create-the-target-database"></a>创建目标数据库

1. 打开 Azure Data Studio，并[连接到大数据群集的 SQL Server 主实例](connect-to-big-data-cluster.md)。

1. 创建新的查询，然后运行以下命令以创建名为 **MyTestDatabase** 的示例数据库。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

### <a name="load-sample-data-into-hdfs"></a>将示例数据加载到 HDFS 中

1. 将 [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) 下载到本地计算机。

1. 启动 Azure Data Studio，并[连接到大数据群集](connect-to-big-data-cluster.md)。

1. 右键单击大数据群集中的 HDFS 文件夹，然后选择“新建目录”  。 将目录命名为“spark_data”  。

1. 右键单击“spark_data”目录，然后选择“上传文件”   。 上传“AdultCensusIncome.csv”文件  。

   ![AdultCensusIncome CSV 文件](./media/spark-mssql-connector/spark_data.png)

### <a name="run-the-sample-notebook"></a>运行示例笔记本

若要演示在非 AD 模式下将适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器与此数据配合使用，可下载示例笔记本，在 Azure Data Studio 中将其打开，然后运行每个代码块。 有关使用笔记本的详细信息，请参阅[如何在 SQL Server 中使用笔记本](../azure-data-studio/notebooks-guidance.md)。

1. 从 PowerShell 或 bash 命令行运行以下命令，以下载“mssql_spark_connector_non_ad_pyspark.ipynb”  示例笔记本：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector_non_ad_pyspark.ipynb"
   ```

1. 在 Azure Data Studio 中，打开示例笔记本文件。 验证它是否已连接到大数据群集的 HDFS/Spark 网关。

1. 运行示例中的每个代码单元，以了解适用于 SQL Server 和 Azure SQL 的 Apache Spark 连接器的用法。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[如何在 Kubernetes 部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)

需要对 SQL Server 大数据群集提供反馈或功能建议？ [请在 SQL Server 大数据群集反馈上给我们留言](https://aka.ms/sql-server-bdc-feedback)。
