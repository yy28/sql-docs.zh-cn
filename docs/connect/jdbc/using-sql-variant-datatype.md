---
title: 使用 Sql_variant 数据类型 |Microsoft Docs
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
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025840"
---
# <a name="using-sql_variant-data-type"></a>使用 Sql_variant 数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从版本 6.3.0, JDBC 驱动程序支持 sql_variant 数据类型。 使用表值参数和 BulkCopy 等功能时, 也支持 Sql_variant, 此页稍后会提到某些限制。 并非所有数据类型都可以存储在 sql_variant 数据类型中。 有关支持 sql_variant 的数据类型的列表, 请查看 SQL Server[文档](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)。

##  <a name="populating-and-retrieving-a-table"></a>填充和检索表:
假设有一个表具有如下所示的 sql_variant 列:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

使用语句插入值的示例脚本:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

使用预定义语句插入值:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果所传递的数据的基础类型已知, 则可以使用各自的资源库。 例如, `preparedStatement.setInt()`可以在插入整数值时使用。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

若要从表中读取值, 可以使用各自的 getter。 例如, 如果`getInt()`来自`getString()`服务器的值已知, 则可以使用或方法:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>将存储过程用于 sql_variant:   
具有如下所示的存储过程:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
必须注册输出参数:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Sql_variant 的限制:
- 当使用 TVP 用存储在 sql_variant 中的`datetime` `date`值填充表`smalldatetime` `getDateTime()` / / 时,/调用`getSmallDateTime()` / `getDate()`结果集不起作用, 并引发以下异常:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    解决方法: `getString()`使用`getObject()`或。 
    
- 不支持使用 TVP 来填充表并在 sql_variant 中发送 null 值, 并且会引发异常:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
