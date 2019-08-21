---
title: 使用大容量复制 API 进行批处理 JDBC 驱动程序的批处理插入操作 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027097"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>将大容量复制 API 用于批量插入操作

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

适用于 SQL Server 的 Microsoft JDBC Driver 7.0 支持使用大容量复制 API 进行 Azure 数据仓库的批量插入操作。 此功能允许用户在执行批处理插入操作时允许驱动程序在下面执行大容量复制操作。 该驱动程序旨在实现性能改进, 同时插入与驱动程序使用定期批处理插入操作时相同的数据。 驱动程序将分析用户的 SQL 查询, 利用大容量复制 API 代替常用的批处理插入操作。 下面介绍了如何通过各种方式为批处理插入功能启用大容量复制 API 以及其限制列表。 此页还包含一个小示例代码, 该代码演示了用法和性能的提高。

此功能仅适用于 java.sql.preparedstatement 和 CallableStatement 的`executeBatch()`  &  `executeLargeBatch()` api。

## <a name="prerequisites"></a>必备条件

为批量插入启用大容量复制 API 有两个先决条件。

* 服务器必须是 Azure 数据仓库。
* 查询必须是插入查询 (查询可能包含注释, 但查询必须以 INSERT 关键字开头才能使此功能生效)。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>启用成批插入的批量复制 API

可以通过三种方式为批处理插入启用批量复制 API。

### <a name="1-enabling-with-connection-property"></a>1.通过连接属性启用

**如果将 useBulkCopyForBatchInsert = true;** 添加到连接字符串, 则会启用此功能。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.通过 SQLServerConnection 对象启用 with setUseBulkCopyForBatchInsert () 方法

调用**SQLServerConnection. setUseBulkCopyForBatchInsert (true)** 将启用此功能。

**SQLServerConnection. getUseBulkCopyForBatchInsert ()** 检索**useBulkCopyForBatchInsert**连接属性的当前值。

对于每个 Java.sql.preparedstatement, **useBulkCopyForBatchInsert**的值在初始化时保持不变。 对**SQLServerConnection ()** 的任何后续调用都不会影响已创建的 java.sql.preparedstatement 相对于其值。

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.通过 SQLServerDataSource 对象启用 with setUseBulkCopyForBatchInsert () 方法

与上面类似, 但使用 SQLServerDataSource 创建 SQLServerConnection 对象。 这两种方法可以得到相同的结果。

## <a name="known-limitations"></a>已知的限制

目前这些限制适用于此功能。

* 不支持包含非参数化值 (例如`INSERT INTO TABLE VALUES (?, 2`) 的 Insert 查询。 通配符 (？) 是此函数支持的唯一参数。
* 不支持包含插入选择表达式的插入查询 (例如`INSERT INTO TABLE SELECT * FROM TABLE2`)。
* 不支持包含多个值表达式 (例如`INSERT INTO TABLE VALUES (1, 2) (3, 4)`) 的 Insert 查询。
* 不支持将后跟 OPTION 子句、与多个表联接或后跟另一个查询的查询插入。
* 由于大`MONEY`容量复制 API、 `DATETIMEOFFSET` `DATE` `DATETIME` 、、`GEOGRAPHY` 、、、、、和数据类型的限制, 目前不支持此`SMALLMONEY` `SMALLDATETIME` `TIME` `GEOMETRY`具有.

如果查询由于非 "SQL server" 相关错误而失败, 则驱动程序将记录错误消息, 并回退到批处理插入的原始逻辑。

## <a name="example"></a>示例

下面是一个示例代码, 演示了在 (常规 vs 大容量复制 API) 方案中针对上千行的 Azure DW 执行批量插入操作的用例。

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

结果：

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序提升性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
