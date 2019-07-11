---
title: 将数据引入到 SQL Server 数据池
titleSuffix: SQL Server big data clusters
description: 本教程演示如何将数据引入到 SQL Server 2019 大数据群集 （预览版） 的数据池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 52881f5102125cc008c1a35278b9bf46bef289f4
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728357"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>教程：将数据引入到 TRANSACT-SQL 的 SQL Server 数据池

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程演示如何使用 TRANSACT-SQL 将数据加载到[数据池](concept-data-pool.md)的 SQL Server 2019 大数据群集 （预览版）。 使用 SQL Server 大数据群集时，可以引入并分布在数据池实例从各种源的数据。

在本教程中，您学习如何：

> [!div class="checklist"]
> * 在数据池中创建外部表。
> * 数据池表中插入示例 web 点击流数据。
> * 带有本地表数据池表中联接数据。

> [!TIP]
> 如果您愿意，可以下载并运行本教程中的所有命令的脚本。 有关说明，请参阅[数据池示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)GitHub 上。

## <a id="prereqs"></a> 先决条件

- [大数据工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
- [将示例数据加载到你的大数据群集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>在数据池中创建外部表

以下步骤创建外部表中名为的数据池**web_clickstream_clicks_data_pool**。 此表可以然后使用作为位置的数据引入到大数据群集。

1. 在 Azure Data Studio，连接到你的大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](connect-to-big-data-cluster.md#master)。

1. 在该连接上双击**服务器**窗口以显示 SQL Server 主实例的服务器仪表板。 选择**新查询**。

   ![SQL Server 主实例查询](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 运行以下 TRANSACT-SQL 命令，以将上下文更改为**销售**主实例中的数据库。

   ```sql
   USE Sales
   GO
   ```

1. 如果尚不存在，请创建到数据池外部数据源。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 创建命名的外部表**web_clickstream_clicks_data_pool**中数据池。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. 在 CTP 3.1 中，数据池创建是异步的但没有方法来确定它尚未完成。 等待两分钟，以确保在继续操作之前创建数据池。

## <a name="load-data"></a>加载数据

以下步骤将示例 web 点击流数据引入到使用前面步骤中创建的外部表的数据池。

1. 使用`INSERT INTO`语句来查询的结果插入到数据池 ( **web_clickstream_clicks_data_pool**外部表)。

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs_parquet
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. 检查与两个 SELECT 查询插入的数据。

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>查询数据

联接中的数据池与在本地数据的查询的存储的结果**销售**表。

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>清理

使用以下命令删除本教程中创建的数据库对象。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>后续步骤

了解如何将数据引入到 Spark 作业具有的数据池：
> [!div class="nextstepaction"]
> [引入数据与 Spark 作业](tutorial-data-pool-ingest-spark.md)
