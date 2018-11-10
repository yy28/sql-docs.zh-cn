---
title: 如何将数据引入到 Spark 作业的 SQL Server 数据池 |Microsoft Docs
description: 本教程演示如何将数据引入到在 Azure Data Studio 中使用 Spark 作业的 SQL Server 2019 大数据群集 （预览版） 的数据池。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: 186de5e63663b9c5485cd0385ded816cafbc7c3d
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221473"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教程： 将数据引入到 Spark 作业的 SQL Server 数据池

本教程演示如何使用 Spark 作业将数据加载到[数据池](concept-data-pool.md)的 SQL Server 2019 大数据群集 （预览版）。 

在本教程中，您学习如何：

> [!div class="checklist"]
> * 在数据池中创建外部表。
> * 创建 Spark 作业以从 HDFS 中加载数据。
> * 查询外部表中的结果。

> [!TIP]
> 如果您愿意，可以下载并运行本教程中的所有命令的脚本。 有关说明，请参阅[数据池示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)GitHub 上。

## <a id="prereqs"></a> 先决条件

* [部署 Kubernetes 上的大数据群集](deployment-guidance.md)。
* [安装 Azure Data Studio 和 SQL Server 2019 扩展](deploy-big-data-tools.md)。
* [将示例数据加载到群集](#sampledata)。

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-in-the-data-pool"></a>在数据池中创建外部表

以下步骤创建外部表中名为的数据池**web_clickstreams_spark_results**。 此表可以然后使用作为位置的数据引入到大数据群集。

1. 在 Azure Data Studio，连接到你的大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](deploy-big-data-tools.md#master)。

1. 在该连接上双击**服务器**窗口以显示 SQL Server 主实例的服务器仪表板。 选择**新查询**。

   ![SQL Server 主实例查询](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 创建命名的外部表**web_clickstreams_spark_results**中数据池。 `SqlDataPool`数据源是可以从任何大数据群集的主实例使用的特殊数据源类型。

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. 在 CTP 2.1 中，数据池创建是异步的但没有方法来确定它尚未完成。 等待两分钟，以确保在继续操作之前创建数据池。

## <a name="start-a-spark-streaming-job"></a>启动 Spark 流式处理作业

下一步是创建 Spark 流式处理作业，将 web 点击流数据从存储池 (HDFS) 加载到数据池中创建的外部表。

1. 在 Azure Data Studio，连接到你的大数据群集的 HDFS/Spark 网关。 有关详细信息，请参阅[连接到 HDFS/Spark 网关](deploy-big-data-tools.md#hdfs)。

1. 中的 HDFS/Spark 网关连接上双击**服务器**窗口。 然后选择**新的 Spark 作业**。

   ![新的 Spark 作业](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. 在中**新的作业**窗口中，输入中的名称**作业名称**字段。

1. 在中**Jar/py 文件**下拉列表中，选择**HDFS**。 然后输入以下 jar 文件路径：

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. 在中**自变量**字段中，输入以下文本，指定到中的 SQL Server 主实例密码`<your_password>`占位符。 

   ```text
   mssql-master-pool-0.service-master-pool 1433 sa <your_password> sales web_clickstreams_spark_results hdfs:///clickstream_data csv false
   ```

   下表描述了每个自变量：

   | 参数 | Description |
   |---|---|
   | 服务器名称 (server name) | SQL 服务器读取表架构，请使用 |
   | 端口号 | SQL Server 端口正在侦听 （默认值为 1433年） |
   | username | SQL Server 登录用户名 |
   | password | SQL Server 登录密码 |
   | 数据库名称 | 目标数据库 |
   | 外部表名称 | 要使用的结果的表 |
   | 流式处理源目录 | 这必须是完整的 URI，如"hdfs: / / clickstream_data" |
   | 输入的格式 | 这可以是"csv"、"parquet"或"json" |
   | 启用检查点 | True 或 False |

1. 按**提交**来提交作业。

   ![Spark 作业提交](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>查询数据

以下步骤说明，Spark 流式处理作业载入数据从 HDFS 数据池。

1. 查询引入的数据之前, 查看的任务历史记录输出以查看该作业已完成。

   ![Spark 作业历史记录](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 返回到本教程开始时打开的 SQL Server 主实例查询窗口...

1. 运行以下查询来检查引入的数据。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>清理

使用以下命令删除本教程中创建的数据库对象。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>后续步骤

了解如何在 Azure Data Studio 中运行示例 notebook:
> [!div class="nextstepaction"]
> [运行示例 notebook](tutorial-notebook-spark.md)
