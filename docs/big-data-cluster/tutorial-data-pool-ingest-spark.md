---
title: 使用 Spark 作业引入数据
titleSuffix: SQL Server big data clusters
description: 本教程演示如何使用 Azure Data Studio 中的 Spark 作业将数据引入到 SQL Server 2019 大数据群集（预览版）的数据池中。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6d0ea6d4fb7a3aea9788c089ad68cb3bf523837f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957817"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教程：使用 Spark 作业将数据引入 SQL Server 数据池

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程演示如何使用 Spark 作业将数据加载到 SQL Server 2019 大数据群集（预览版）的[数据池](concept-data-pool.md)。 

在本教程中，你将学习如何执行以下操作：

> [!div class="checklist"]
> * 在数据池中创建外部表。
> * 创建 Spark 作业以从 HDFS 加载数据。
> * 在外部表中查询结果。

> [!TIP]
> 如果需要，可以下载并运行本教程中的命令脚本。 有关说明，请参阅 GitHub 上的[数据池示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)。

## <a id="prereqs"></a> 先决条件

- [大数据工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
- [将示例数据加载到大数据群集中](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>在数据池中创建外部表

以下步骤会在数据池中创建一个名为“web_clickstreams_spark_results”的外部表  。 然后，可以将此表用作将数据引入到大数据群集的位置。

1. 在 Azure Data Studio 中，连接到大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](connect-to-big-data-cluster.md#master)。

1. 双击“服务器”窗口中的连接，以显示 SQL Server 主实例的服务器仪表板  。 选择“新建查询”  。

   ![SQL Server 主实例查询](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. 如果尚未创建数据池的外部数据源，请创建该数据源。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 在数据池中创建一个名为“web_clickstreams_spark_results”的外部表  。

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
  
1. 在 CTP 3.1 中，数据池的创建是异步的，但无法确定其完成时间。 等待两分钟，确保在继续操作之前已创建数据池。

## <a name="start-a-spark-streaming-job"></a>启动 Spark 流式处理作业

下一步是创建一个 Spark 流式处理作业，将 Web 点击流数据从存储池 (HDFS) 加载到你在数据池中创建的外部表。

1. 在 Azure Data Studio 中，连接到大数据群集的主实例。 有关详细信息，请参阅[连接到大数据群集](connect-to-big-data-cluster.md)。

1. 双击“服务器”窗口中的 HDFS/Spark 网关连接  。 然后选择“新建 Spark 作业”  。

   ![新建 Spark 作业](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. 在“新建作业”窗口的“作业名称”字段中输入一个名称   。

1. 在“Jar/py 文件”下拉列表中，选择“HDFS”   。 然后输入以下 jar 文件路径：

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. 在“主类”字段中，输入 `FileStreaming`  。

1. 在“参数”字段中，输入以下文本，并在 `<your_password>` 占位符中指定 SQL Server 主实例的密码  。 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   下表对每个参数进行了说明：

   | 参数 | 描述 |
   |---|---|
   | 服务器名称 (server name) | 用于读取表架构的 SQL Server |
   | 端口号 | SQL Server 正在侦听的端口（默认为 1433） |
   | username | SQL Server 登录用户名 |
   | password | SQL Server 登录密码 |
   | 数据库名称 | 目标数据库 |
   | 外部表名 | 要用于结果的表 |
   | 要流式处理的源目录 | 这必须是完整的 URI，例如“hdfs:///clickstream_data” |
   | 输入格式 | 这可以是“csv”、“parquet”或“json” |
   | 启用检查点 | True 或 False |
   | timeout | 退出前运行作业的时间（以毫秒为单位） |

1. 按“提交”提交作业  。

   ![Spark 作业提交](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>查询数据

以下步骤演示了 Spark 流式处理作业将数据从 HDFS 加载到数据池中。

1. 在查询引入的数据前，查看任务历史记录输出，了解作业是否已完成。

   ![Spark 作业历史记录](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. 返回到本教程开头部分打开的 SQL Server 主实例查询窗口。

1. 运行以下查询以检查引入的数据。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>清除

使用以下命令删除本教程中创建的数据库对象。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>后续步骤

了解如何在 Azure Data Studio 中运行示例笔记本：
> [!div class="nextstepaction"]
> [运行示例笔记本](tutorial-notebook-spark.md)
