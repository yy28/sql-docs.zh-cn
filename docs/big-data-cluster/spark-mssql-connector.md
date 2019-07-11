---
title: 将 Spark 连接到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何在 Spark 中使用 MSSQL Spark 连接器来读取和写入到 SQL Server。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aaa9cd54c3540c17f9995f985f4537dafe05d5c2
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727471"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>如何读取和写入到 SQL Server 从 Spark 使用 MSSQL Spark 连接器

密钥的大数据使用模式是在 Spark 中，然后将数据写入 SQL Server 访问业务线应用程序的大容量数据处理。 这些使用情况模式受益于利用关键的 SQL 优化，并提供了高效的写机制的连接器。

本文提供了如何使用 MSSQL Spark 连接器来读取和写入大数据群集中的以下位置的示例：

1. SQL Server 主实例
1. SQL Server 数据池

   ![MSSQL Spark 连接器关系图](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

该示例将执行以下任务：

- 从 HDFS 中读取文件并进行一些基本的处理。
- 数据帧写入为 SQL 表的 SQL Server 主实例，然后阅读到数据帧的表。
- 将数据帧写入到 SQL 外部表作为 SQL Server 数据池，然后阅读到数据帧的外部表。

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 连接器接口

SQL Server 2019 预览提供了**MSSQL Spark 连接器**适用于大数据群集使用 SQL Server 大容量 Api 的写入 Spark SQL 写入。 MSSQL Spark 连接器基于 Spark 数据源的 Api，并提供熟悉的 Spark JDBC 连接器界面。 有关接口参数，请参阅[Apache Spark 文档](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 按名称引用 MSSQL Spark 连接器**com.microsoft.sqlserver.jdbc.spark**。

下表描述已更改或新接口参数：

| 属性名称 | 可选 | 描述 |
|---|---|---|
| **isolationLevel** | 是 | 此部分描述连接的隔离级别。 默认值为 MSSQLSpark 连接器**READ_COMMITTED** |

连接器使用 SQL Server 大容量编写 Api。 参数可以作为可选参数传递的用户和作为传递的任何大容量写入-是由到基础 API 连接器。 有关大容量的详细信息写入操作，请参阅[SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="prerequisites"></a>先决条件

- 一个[SQL Server 大数据群集](deploy-get-started.md)。

- [Azure 数据 Studio](https://aka.ms/azdata-insiders)。

## <a name="create-the-target-database"></a>创建目标数据库

1. 打开 Azure Data Studio，并[连接到你的大数据群集的 SQL Server 主实例](connect-to-big-data-cluster.md)。

1. 创建一个新查询，并运行以下命令以创建一个名为的示例数据库**MyTestDatabase**。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>将示例数据加载到 HDFS

1. 下载[AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv)到本地计算机。

1. 启动 Azure Data Studio，并[连接到你的大数据群集](connect-to-big-data-cluster.md)。

1. 在大数据群集上的 HDFS 文件夹上右键单击并选择**的新目录**。 目录命名**spark_data**。

1. 右键单击**spark_data**目录，然后选择**将文件上传**。 上传**AdultCensusIncome.csv**文件。

   ![AdultCensusIncome CSV 文件](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>运行示例 notebook

若要演示如何使用此数据的 MSSQL Spark 连接器，可以下载示例 notebook、 Azure Data Studio 中将其打开并运行每个代码块。 有关使用笔记本的详细信息，请参阅[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。

1. 从 PowerShell 或 bash 命令行运行以下命令，下载**mssql_spark_connector.ipynb**示例 notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. 在 Azure Data Studio，打开示例 notebook 文件。 验证它已连接到你的大数据群集在 HDFS/Spark 网关。

1. 运行示例，了解有关使用 MSSQL Spark 连接器中的每个代码单元。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)