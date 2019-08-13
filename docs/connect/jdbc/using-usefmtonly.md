---
title: 通过 useFmtOnly 检索 Java.sql.parametermetadata |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 29ee2c5c22baf77b6994a440f1d9d442ba2b812a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894089"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>通过 useFmtOnly 检索 Java.sql.parametermetadata
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC Driver for SQL Server 包含从服务器**useFmtOnly**查询参数元数据的另一种方法。 此功能是在驱动程序版本7.4 中首次引入的, 并需要作为中`sp_describe_undeclared_parameters`已知问题的解决方法。
  
  驱动程序主要使用该存储过程`sp_describe_undeclared_parameters`来查询参数元数据, 因为在大多数情况下, 使用这种方法来检索参数元数据。 但是, 在以下用例中, 当前执行存储过程会失败:
  
-   针对 Always Encrypted 列
  
-   针对临时表和表变量
  
-   针对视图 
  
  针对这些用例的建议的解决方案是, 分析用户的参数和表目标的 SQL 查询, 然后执行`SELECT` `FMTONLY`启用的查询。 以下代码片段将帮助可视化此功能。
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>打开/关闭功能 
 默认情况下, 功能**useFmtOnly**处于关闭状态。 用户可以通过指定`useFmtOnly=true`连接字符串来启用此功能。 例如： `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`。
 
 或者, 通过`SQLServerDataSource`提供此功能。
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 此功能也可用于语句级别。 用户可以通过`PreparedStatement.setUseFmtOnly(boolean)`打开/关闭功能。
> [!NOTE]  
>  驱动程序将对 "连接级别" 属性的 "语句级别" 属性设置优先级。

## <a name="using-the-feature"></a>使用功能
  启用后, 驱动程序将在内部开始使用新功能, 而`sp_describe_undeclared_parameters`不是查询参数元数据。 最终用户不需要执行任何其他操作。
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  此功能仅支持`SELECT/INSERT/UPDATE/DELETE`查询。 查询应以4个支持的关键字之一开始, 或使用一个受支持的查询的[公用表表达式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017)。 不支持公用表表达式中的参数。

## <a name="known-issues"></a>已知问题
  此功能当前存在一些问题，是由 SQL 分析逻辑中的缺陷导致的。 此功能的未来更新可能会解决这些问题, 并在下面提供解决方法建议。
  
A. 使用 "前向声明" 别名
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. 当表具有共享列名时, 列名称不明确
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. 从包含参数的子查询中选择
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. SET 子句中的子查询
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>另请参阅  
 [设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
