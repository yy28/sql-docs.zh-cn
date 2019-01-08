---
title: 在 Oracle 中的查询外部数据
titleSuffix: SQL Server 2019 big data clusters
description: 本教程演示如何查询从 SQL Server 2019 大数据群集 （预览版） 的 Oracle 数据。 你对 Oracle 中的数据创建外部表，然后运行查询。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: tutorial
ms.custom: seodec18
ms.openlocfilehash: f7a367a41814a7cb590276b10fcfb7c4c8697011
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432150"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>教程：从 SQL Server 大数据群集查询 Oracle

本教程演示如何查询 SQL Server 2019 大数据群集中的 Oracle 数据。 若要运行本教程中，您需要有权访问 Oracle 服务器。 如果你没有访问权限，本教程可使您的数据虚拟化的 SQL Server 大数据群集中的外部数据源的工作方式。

在本教程中，您学习如何：

> [!div class="checklist"]
> * 外部 Oracle 数据库中创建外部表的数据。
> * 将此数据与高价值的数据联接主实例中。

> [!TIP]
> 如果您愿意，可以下载并运行本教程中的所有命令的脚本。 有关说明，请参阅[数据虚拟化示例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)GitHub 上。

## <a id="prereqs"></a> 先决条件

- [大数据工具](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
- [将示例数据加载到你的大数据群集](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>创建 Oracle 表

以下步骤创建名为的示例表`INVENTORY`在 Oracle 中。

1. 连接到 Oracle 实例和你想要使用本教程中的数据库。

1. 运行以下语句以创建`INVENTORY`表：

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. 导入的内容**inventory.csv**到此表中的文件。 此文件创建的示例创建脚本[先决条件](#prereqs)部分。

## <a name="create-an-external-data-source"></a>创建外部数据源

第一步是创建可以访问你的 Oracle 服务器的外部数据源。

1. 在 Azure Data Studio，连接到你的大数据群集的 SQL Server 主实例。 有关详细信息，请参阅[连接到 SQL Server 主实例](connect-to-big-data-cluster.md#master)。

1. 在该连接上双击**服务器**窗口以显示 SQL Server 主实例的服务器仪表板。 选择**新查询**。

   ![SQL Server 主实例查询](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 运行以下 TRANSACT-SQL 命令，以将上下文更改为**销售**主实例中的数据库。

   ```sql
   USE Sales
   GO
   ```

1. 创建数据库范围的凭据以连接到 Oracle 服务器。 提供到下面的语句中的 Oracle 服务器的相应凭据。

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. 创建指向 Oracle 服务器的外部数据源。

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>创建外部表

接下来，创建名为的外部表**iventory_ora**转移`INVENTORY`Oracle 服务器上的表。

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> 表名称和列名称将使用 ANSI SQL 查询针对 Oracle 时带引号的标识符。 因此，名称是区分大小写。 请务必在与 Oracle 元数据中的表和列名称的正确大小写相匹配的外部表定义中指定的名称。

## <a name="query-the-data"></a>查询数据

运行以下查询联接数据`iventory_ora`本地中的表的外部表`Sales`数据库。

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>清理

使用以下命令删除本教程中创建的数据库对象。

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>后续步骤

了解如何将数据引入到数据池：
> [!div class="nextstepaction"]
> [将数据加载到数据池](tutorial-data-pool-ingest-sql.md)
