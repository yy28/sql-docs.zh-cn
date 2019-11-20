---
title: 使用 Spark 作业引入数据
titleSuffix: SQL Server big data clusters
description: 本教程演示如何使用 Azure Data Studio 中的 Spark 作业将数据引入到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的数据池中。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6f66b42fe280ef6612a5e9974ddcf4f1f7ccfcb
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119194"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>教程：使用 Spark 作业将数据引入 SQL Server 数据池

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程演示如何使用 Spark 作业将数据加载到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的[数据池](concept-data-pool.md)。 

在本教程中，你将了解如何执行以下操作：

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
   USE Sales
   GO
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

下一步是创建一个 Spark 流式处理作业，将 Web 点击流数据从存储池 (HDFS) 加载到你在数据池中创建的外部表。 此数据已添加到[将示例数据加载到大数据群集](tutorial-load-sample-data.md)中的 /clickstream_data。

1. 在 Azure Data Studio 中，连接到大数据群集的主实例。 有关详细信息，请参阅[连接到大数据群集](connect-to-big-data-cluster.md)。

2. 创建新笔记本并选择 Spark | Scala 作为内核。

3. 运行 Spark 引入作业
   1. 配置 Spark-SQL 连接器参数
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",LongType,true), StructField("wcs_click_time_sk",LongType,true), 
      StructField("wcs_sales_sk",LongType,true), StructField("wcs_item_sk",LongType,true),
      StructField("wcs_web_page_sk",LongType,true), StructField("wcs_user_sk",LongType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. 定义并运行 Spark 作业
      * 每个作业都有两部分：readStream 和 writeStream。 下面，我们使用上面定义的架构创建数据帧，然后将其写入到数据池中的外部表。
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.processAllAvailable()
      query.awaitTermination(40000)
      ```
## <a name="query-the-data"></a>查询数据

以下步骤演示了 Spark 流式处理作业将数据从 HDFS 加载到数据池中。

1. 在查询引入的数据之前，请查看 Spark 执行状态（包括 Yarn 应用 ID、Spark UI 和驱动程序日志）。

   ![Spark 执行详细信息](./media/tutorial-data-pool-ingest-spark/Spark-Joblog-sparkui-yarn.png)

1. 返回到本教程开头部分打开的 SQL Server 主实例查询窗口。

1. 运行以下查询以检查引入的数据。

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```
1. 还可以在 Spark 中查询数据。 例如，下面的代码将打印表中记录的数量：
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
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
