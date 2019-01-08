---
title: 查询存储池中的 HDFS 数据
titleSuffix: SQL Server 2019 big data clusters
description: 本教程演示如何查询 SQL Server 2019 大数据群集 （预览版） 中的 HDFS 数据。 你对在存储池中的数据创建外部表，然后运行查询。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 78b78fafa8b2dce197fae98ef42b763cc0fa2f4e
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432170"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>教程：在 SQL Server 大数据群集中的查询 HDFS

本教程演示如何查询 SQL Server 2019 大数据群集 （预览版） 中的 HDFS 数据。

在本教程中，您学习如何：

> [!div class="checklist"]
> * 创建外部表指向 HDFS 的大数据群集中的数据。
> * 将此数据与高价值的数据联接主实例中。

> [!TIP]
> 如果您愿意，可以下载并运行本教程中的所有命令的脚本。 有关说明，请参阅[数据虚拟化示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)GitHub 上。

## <a id="prereqs"></a> 先决条件

- [大数据工具](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
- [将示例数据加载到你的大数据群集](tutorial-load-sample-data.md)

## <a name="create-an-external-table-to-hdfs"></a>创建到 HDFS 的外部表

存储池包含 web 点击流数据存储在 HDFS 中的 CSV 文件中。 使用以下步骤来定义可以访问该文件中的数据的外部表。

1. 在 Azure Data Studio，连接到你的大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](connect-to-big-data-cluster.md#master)。

2. 在该连接上双击**服务器**窗口以显示 SQL Server 主实例的服务器仪表板。 选择**新查询**。

   ![SQL Server 主实例查询](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

3. 运行以下 TRANSACT-SQL 命令，以将上下文更改为**销售**主实例中的数据库。

   ```sql
   USE Sales
   GO
   ```

4. 定义要从 HDFS 读取的 CSV 文件格式。 按 F5 运行该语句。

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

5. 创建外部表可以读取`/clickstream_data`从存储池。 **SqlStoragePool**可从大数据群集的主实例进行访问。

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>查询数据

运行以下查询加入 HDFS 数据`web_clickstream_hdfs`本地中的关系数据的外部表`Sales`数据库。

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>清理

使用以下命令删除本教程中使用的外部表。

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>后续步骤

转到下一步的文章，了解如何从大数据群集查询 Oracle。
> [!div class="nextstepaction"]
> [在 Oracle 中的查询外部数据](tutorial-query-oracle.md)
