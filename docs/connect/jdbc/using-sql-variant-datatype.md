---
title: 使用 Sql_variant 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c004bc40ed0c85b82612be9069e1a53041c8095c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798586"
---
# <a name="using-sqlvariant-data-type"></a>使用 sql_variant 数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从版本 6.3.0，JDBC 驱动程序支持 sql_variant 数据类型。 使用具有某些限制的功能，如表值参数和 BulkCopy 提到稍后在此页时，也支持 Sql_variant。 并非所有数据类型可以都存储在 sql_variant 数据类型。 使用 sql_variant 的受支持的数据类型的列表，请检查 SQL Server [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)。

##  <a name="populating-and-retrieving-a-table"></a>填充和检索表：
假设某个具有 sql_variant 列作为包含的表：

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

用于使用语句插入值的示例脚本：

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

插入值使用预定义语句：

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果已知正在传递的数据的基础类型，可以使用相应的 setter。 例如，`preparedStatement.setInt()`可以插入一个整数值时使用。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

用于从表中读取值，可以使用相应的 getter。 例如，`getInt()`或`getString()`如果来自服务器的值已知的则可以使用方法：    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>使用 sql_variant 存储的过程：   
例如具有存储的过程：     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
必须注册输出参数：

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sqlvariant"></a>Sql_variant 的限制：
- 当使用 TVP 填充一个表与`datetime` / `smalldatetime` / `date` sql_variant 中存储值调用`getDateTime()` / `getSmallDateTime()` / `getDate()`上结果集不起作用，并引发以下异常：
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    解决方法： 使用`getString()`或`getObject()`相反。 
    
- 使用 TVP 填充一个表和 sql_variant 中发送 null 值不受支持并且引发异常：
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
