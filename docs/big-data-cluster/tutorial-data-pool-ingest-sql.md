---
title: 将数据引入 SQL Server 数据池
titleSuffix: SQL Server big data clusters
description: 本教程演示如何将数据引入 SQL Server 2019 大数据群集（预览版）数据池中。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 178eceaf99d1f8c2b51f7079d0bdd406c2cb5eef
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670520"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>教程：使用 Transact-SQL 将数据引入 SQL Server 数据池

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程演示如何使用 Transact-SQL 将数据加载到 SQL Server 2019 大数据群集（预览版）的[数据池](concept-data-pool.md)。 使用 SQL Server 大数据群集，可以跨数据池实例引入和分布来自各种源的数据。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> * 在数据池中创建外部表。
> * 将示例 Web 点击流数据插入到数据池表中。
> * 将数据池中的数据与本地表联接在一起。

> [!TIP]
> 如果需要，可以下载并运行本教程中的命令脚本。 有关说明，请参阅 GitHub 上的[数据池示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool)。

## <a id="prereqs"></a> 先决条件

- [大数据工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
- [将示例数据加载到大数据群集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>在数据池中创建外部表

以下步骤将在名为 web_clickstream_clicks_data_pool 的数据池中创建一个外部表。 然后，可以将此表用作将数据引入到大数据群集的位置。

1. 在 Azure Data Studio 中，连接到大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](connect-to-big-data-cluster.md#master)。

1. 双击“服务器”窗口中的连接以显示 SQL Server 主实例的服务器仪表板。 选择“新建查询”。

   ![SQL Server 主实例查询](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 运行以下 Transact-SQL 命令，将上下文更改为主实例中的 Sales 数据库。

   ```sql
   USE Sales
   GO
   ```

1. 如果尚未创建数据池的外部数据源，请创建该数据源。

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. 在数据池中创建一个名为 web_clickstream_clicks_data_pool 的外部表。

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
  
1. 在 CTP 3.1 中，数据池的创建是异步的，但还无法确定其完成时间。 等待两分钟，确保在数据池创建完成之后再继续。

## <a name="load-data"></a>加载数据

以下步骤使用在先前步骤中创建的外部表将示例 Web 点击流数据引入该数据池。

1. 使用 `INSERT INTO` 语句将查询结果插入数据池（web_clickstream_clicks_data_pool 外部表）。

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. 使用两个 SELECT 查询检查插入的数据。

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>查询数据

在包含 Sales 表中本地数据的数据池中，联接查询的存储结果。

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

## <a name="clean-up"></a>清除

使用以下命令删除本教程中创建的数据库对象。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>后续步骤

了解如何通过 Spark 作业将数据引入到数据池中：
> [!div class="nextstepaction"]
> [使用 Spark 作业引入数据](tutorial-data-pool-ingest-spark.md)
