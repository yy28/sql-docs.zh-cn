---
title: 使用基本数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83bbe2c28e9b353e5a82fa630660756174ad0dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916362"
---
# <a name="using-basic-data-types"></a>使用基本数据类型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 使用 JDBC 基本数据类型将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型转换为 Java 编程语言能够理解的格式，反之亦然。 JDBC 驱动程序提供对 JDBC 4.0 API 的支持, 其中包括**SQLXML**数据类型和国家 (Unicode) 数据类型 (如**NCHAR**、 **NVARCHAR**、 **LONGNVARCHAR**和**NCLOB**)。  
  
## <a name="data-type-mappings"></a>数据类型映射

下表列出了基本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC 和 Java 编程语言数据类型之间的默认映射：  
  
| SQL Server 类型   | JDBC 类型 (java.sql.Types)                        | Java 语言类型          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| BINARY             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| 日期               | DATE                                               | java.sql.Date                |
| DATETIME           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| Decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| 图像              | LONGVARBINARY                                      | byte[]                       |
| INT                | 整数                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| REAL               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| TIMESTAMP          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| geometry           | VARBINARY                                          | byte[]                       |
| 地理          | VARBINARY                                          | byte[]                       |
  
(1) 若要将 java.sql.Time 与时间 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型一起使用，必须将 sendTimeAsDatetime 连接属性设置为 false  。  
  
(2) 可以使用[Datetimeoffset 类](../../connect/jdbc/reference/datetimeoffset-class.md)以编程方式访问**datetimeoffset**值。  
  
以下几部分提供了如何使用 JDBC 驱动程序和基本数据类型的示例。 有关如何在 Java 应用程序中使用基本数据类型的更多详细示例，请参阅[基本数据类型示例](../../connect/jdbc/basic-data-types-sample.md)。  
  
## <a name="retrieving-data-as-a-string"></a>以字符串的格式检索数据

如果必须从映射到任意 JDBC 基本数据类型的数据源检索数据，并以字符串的格式查看这些数据，或者如果不需要强类型的数据，则可以使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 类的 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 方法，如下所示：  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>按数据类型检索数据

如果必须从数据源检索数据，并且已知检索的数据类型，则应使用 SQLServerResultSet 类的任一 get\<Type> 方法（也称为 Getter 方法）  。 通过 get\<Type> 方法，可以使用列名或列索引，如下所示：  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> 使用扩展方法的 getUnicodeStream 和 getBigDecimal 已被弃用, JDBC 驱动程序不支持这些方法。

## <a name="updating-data-by-data-type"></a>按数据类型更新数据

如果必须更新数据源中字段的值, 请使用 SQLServerResultSet 类的一个更新\<类型 > 方法。 在下面的示例中，[updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) 方法与 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法结合使用，用于更新数据源中的数据：  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> JDBC Driver 无法更新列名长度超过 127 个字符的 SQL Server 列。 如果尝试更新名称长度超过 127 个字符的列，将引发异常。  
  
## <a name="updating-data-by-parameterized-query"></a>通过参数化查询来更新数据

如果必须通过使用参数化查询来更新数据源中的数据，可以使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类的任一 set\<Type> 方法（也称为 setter 方法）来设置参数的数据类型  。 在下面的示例中，[prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 方法用于预编译参数化查询，然后在调用 [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) 方法前，使用 [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) 方法来设置参数的字符串值。  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
有关参数化查询的详细信息, 请参阅[使用带参数的 SQL 语句](../../connect/jdbc/using-an-sql-statement-with-parameters.md)。  

## <a name="passing-parameters-to-a-stored-procedure"></a>向存储过程传递参数

如果必须向存储过程传递类型参数，则可使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的任一 set\<Type> 方法通过索引或名称来设置此参数。 在下面的示例中，[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法用于设置对存储过程的调用，然后在调用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法之前，使用 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 方法设置调用的参数。  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> 在此实例中，将返回一个结果集，包含此存储过程的运行结果。

有关将 JDBC 驱动程序与存储过程和输入参数一起使用的详细信息, 请参阅[使用具有输入参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)。  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>从存储过程检索参数

如果必须从存储过程检索参数，则必须首先使用 SQLServerCallableStatement 类的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法通过名称或索引注册一个输出参数，然后在调用存储过程后，将返回的输出参数分配给合适的变量。 在下面的示例中，使用 prepareCall 方法设置对存储过程的调用，使用 registerOutParameter 方法设置输出参数，然后在调用 executeQuery 方法前，使用 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 方法设置调用的参数。 使用 [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) 方法来检索存储过程的输出参数返回的值。  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> 除返回的输出参数外，还可能返回一个结果集，包含此存储过程的运行结果。  
  
有关如何将 JDBC 驱动程序用于存储过程和输出参数的详细信息, 请参阅将[存储过程与 Output 参数一起使用](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)。  

## <a name="see-also"></a>另请参阅

[了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
