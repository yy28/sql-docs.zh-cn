---
title: 使用大容量复制 API 用于为 MSSQL JDBC 驱动程序的批量插入操作 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 347ce28dc28016f95de2795bd2f5e491dd29e2d8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802638"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>将大容量复制 API 用于批插入操作

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SQL Server 支持对批处理插入操作的 Azure 数据仓库中使用大容量复制 API 的 Microsoft JDBC 驱动程序 7.0。 此功能允许用户启用驱动程序来执行大容量复制操作时执行的批处理插入操作下。 驱动程序旨在提高性能，同时插入相同的数据，如驱动程序必须与正则批中插入操作。 该驱动程序将分析用户的 SQL 查询，利用大容量复制 API 而不是常用的批量插入操作。 以下是各种方法，以启用批处理大容量复制 API 插入功能，以及其自身的局限性的列表。 此页还包含演示使用情况和性能提升以及一个小型示例代码。

此功能仅适用于 PreparedStatement 和 CallableStatement 的`executeBatch()`  &  `executeLargeBatch()` Api。

## <a name="pre-requisites"></a>先决条件

有两个先决条件，为批插入启用大容量复制 API。

* 服务器必须是 Azure 数据仓库。
* 查询必须插入查询 （查询可以包含注释，但查询必须使用此功能生效的插入关键字启动）。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>为批插入启用大容量复制 API

有三种方法，为批插入启用大容量复制 API。

### <a name="1-enabling-with-connection-property"></a>1.启用连接属性

添加**useBulkCopyForBatchInsert = true;** 到连接字符串，此功能。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.启用使用 SQLServerConnection 对象 setUseBulkCopyForBatchInsert() 方法

调用**SQLServerConnection.setUseBulkCopyForBatchInsert(true)** 启用此功能。

**SQLServerConnection.getUseBulkCopyForBatchInsert()** 检索的当前值**useBulkCopyForBatchInsert**连接属性。

值**useBulkCopyForBatchInsert**保持不变的每个 PreparedStatement 在其初始化时。 对任何后续调用**SQLServerConnection.setUseBulkCopyForBatchInsert()** 将不会影响在已创建的 PreparedStatement 关于它的值。

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.启用使用 SQLServerDataSource 对象 setUseBulkCopyForBatchInsert() 方法

与上述相似，但使用 SQLServerDataSource 创建 SQLServerConnection 对象。 这两种方法可以得到相同的结果。

## <a name="known-limitations"></a>已知的限制

目前有以下限制适用于此功能。

* 插入包含非参数化值的查询 (例如， `INSERT INTO TABLE VALUES (?, 2`))，不受支持。 通配符 （？） 是此函数的唯一受支持的参数。
* 插入包含 INSERT SELECT 表达式的查询 (例如， `INSERT INTO TABLE SELECT * FROM TABLE2`)，不受支持。
* 插入包含多个值表达式的查询 (例如， `INSERT INTO TABLE VALUES (1, 2) (3, 4)`)，不受支持。
* 不支持的 OPTION 子句后跟、 联接多个表或另一个查询后, 跟 insert 查询。
* 由于大容量复制 API 的限制`MONEY`， `SMALLMONEY`， `DATE`， `DATETIME`， `DATETIMEOFFSET`， `SMALLDATETIME`， `TIME`， `GEOMETRY`，和`GEOGRAPHY`此当前不支持数据类型功能。

如果查询失败由于非"SQL server"相关的错误，该驱动程序将记录错误消息和回退到批插入的原始逻辑。

## <a name="example"></a>示例

下面是演示批量插入操作针对 Azure DW 的 1000 个行，这两种 (正则 vs 大容量复制 API) 方案的用例的示例代码。

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

[借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
