---
title: 使用 Sql_variant 数据类型 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 081e7d5a4c2c2b2620422e53c91c1e54abd272fa
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923983"
---
# <a name="using-sql_variant-data-type"></a>使用 Sql_variant 数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

从版本 6.3.0 开始，JDBC 驱动程序支持 sql_variant 数据类型。 使用表值参数和 BulkCopy 等功能时，也支持 Sql_variant，本页后面部分将提到一些限制。 并非所有数据类型都可以存储在 sql_variant 数据类型中。 有关 sql_variant 支持的数据类型列表，请查看 SQL Server [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)。

##  <a name="populating-and-retrieving-a-table"></a>填充和检索表：
假设一个表中包含 sql_variant 列，如下所示：

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

使用语句插入值的示例脚本：

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

使用预定义语句插入值：

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果所传递的数据的基础类型已知，则可以使用相应的资源库。 例如，在插入整数值时，可以使用 `preparedStatement.setInt()`。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

若要从表中读取值，可以使用相应的 getter。 例如，如果来自服务器的值已知，则可以使用 `getInt()` 或 `getString()` 方法：    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>使用带有 sql_variant 的存储过程：   
具有如下所示的存储过程：     

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

## <a name="limitations-of-sql_variant"></a>sql_variant 限制：
- 当使用 TVP 用存储在 sql_variant 中的 `datetime`/`smalldatetime`/`date` 值填充表时，在 ResultSet 上调用 `getDateTime()`/`getSmallDateTime()`/`getDate()` 将无效，并且会引发以下异常：
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    解决方法：改为使用 `getString()` 或 `getObject()`。 
    
- 不支持使用 TVP 来填充表并在 sql_variant 中发送 null 值，并且会引发以下异常：
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
