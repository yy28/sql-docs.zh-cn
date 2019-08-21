---
title: 将 Spark 连接到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何使用 Spark 中的 MSSQL Spark 连接器对 SQL Server 执行读写操作。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad3a0e03c75f7961864f70fc52655e47e2b89ea
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653304"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-mssql-spark-connector"></a>如何使用 MSSQL Spark 连接器从 Spark 对 SQL Server 执行读写操作

Spark 中的大容量数据处理是一种关键大数据使用模式，之后会将数据写入 SQL Server 以访问业务线应用程序。 这些使用模式受益于使用关键 SQL 优化并提供高效写入机制的连接器。

本文提供示例，说明如何使用 MSSQL Spark 连接器对大数据群集中的以下位置执行读写操作：

1. SQL Server 主实例
1. SQL Server 数据池

   ![MSSQL Spark 连接器示意图](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

本示例执行以下任务：

- 从 HDFS 读取文件并进行一些基本处理。
- 将数据帧作为 SQL 表写入 SQL Server 主实例，然后将表读取到数据帧。
- 将数据帧作为 SQL 外部表写入 SQL Server 数据池，然后将外部表读取到数据帧。

## <a name="mssql-spark-connector-interface"></a>MSSQL Spark 连接器接口

SQL Server 2019 预览版为大数据群集提供 **MSSQL Spark 连接器**，该连接器使用 SQL Server 批量写入 API 执行 Spark 到 SQL 的写入操作。 MSSQL Spark 连接器基于 Spark 数据源 API，并提供熟悉的 Spark JDBC 连接器接口。 有关接口参数，请参阅 [Apache Spark 文档](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 MSSQL Spark 连接器以 **com.microsoft.sqlserver.jdbc.spark** 这一名称被引用。

下表介绍已更改或新增的接口参数：

| 属性名 | 可选 | 描述 |
|---|---|---|
| **isolationLevel** | 是 | 此参数描述连接的隔离级别。 MSSQL Spark 连接器的默认值为 **READ_COMMITTED** |

连接器使用 SQL Server 批量写入 API。 任何批量写入参数都可由用户作为可选参数进行传递，并可由连接器按原样传递到基础 API。 有关批量写入操作的详细信息，请参阅 [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="prerequisites"></a>先决条件

- [SQL Server 大数据群集](deploy-get-started.md)。

- [Azure Data Studio](https://aka.ms/azdata-insiders)。

## <a name="create-the-target-database"></a>创建目标数据库

1. 打开 Azure Data Studio，并[连接到大数据群集的 SQL Server 主实例](connect-to-big-data-cluster.md)。

1. 创建新的查询，然后运行以下命令以创建名为 **MyTestDatabase** 的示例数据库。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

## <a name="load-sample-data-into-hdfs"></a>将示例数据加载到 HDFS 中

1. 将 [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) 下载到本地计算机。

1. 启动 Azure Data Studio，并[连接到大数据群集](connect-to-big-data-cluster.md)。

1. 右键单击大数据群集中的 HDFS 文件夹，然后选择“新建目录”。 将目录命名为“spark_data”。

1. 右键单击“spark_data”目录，然后选择“上传文件”。 上传“AdultCensusIncome.csv”文件。

   ![AdultCensusIncome CSV 文件](./media/spark-mssql-connector/spark_data.png)

## <a name="run-the-sample-notebook"></a>运行示例笔记本

若要演示如何将 MSSQL Spark 连接器与此数据配合使用，可下载示例笔记本，在 Azure Data Studio 中打开它，然后运行每个代码块。 有关使用笔记本的详细信息，请参阅[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。

1. 从 PowerShell 或 bash 命令行运行以下命令，以下载“mssql_spark_connector.ipynb”示例笔记本：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector.ipynb"
   ```

1. 在 Azure Data Studio 中，打开示例笔记本文件。 验证它是否已连接到大数据群集的 HDFS/Spark 网关。

1. 运行示例中的每个代码单元以查看 MSSQL Spark 连接器的使用情况。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息, 请参阅[如何在[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Kubernetes 上部署](deployment-guidance.md)