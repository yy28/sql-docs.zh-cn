---
title: 使用基本数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab39b74b4e5a2c243622bbd352a71c943e07a3d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-basic-data-types"></a>使用基本数据类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用 JDBC 基本数据类型将转换[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]为 Java 编程语言中，反之亦然可以理解的格式的数据类型。 JDBC 驱动程序支持 JDBC 4.0 API，其中包括**SQLXML**数据类型和美国国家 (Unicode) 数据类型，如**NCHAR**， **NVARCHAR**， **LONGNVARCHAR**，和**NCLOB**。  
  
## <a name="data-type-mappings"></a>数据类型映射  
 下表列出了基本之间的默认映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，JDBC 和 Java 编程语言的数据类型：  
  
|SQL Server 类型|JDBC 类型 (java.sql.Types)|Java 语言类型|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|BINARY|BINARY|byte[]|  
|bit|BIT|boolean|  
|char|CHAR|字符串|  
|date|DATE|java.sql.Date|  
|datetime|TIMESTAMP|java.sql.Timestamp|  
|datetime2|TIMESTAMP|java.sql.Timestamp|  
|datetimeoffset (2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|图像|LONGVARBINARY|byte[]|  
|int|整数|int|  
|money|DECIMAL|java.math.BigDecimal|  
|NCHAR|CHAR<br /><br /> NCHAR (Java SE 6.0)|字符串|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|字符串|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|字符串|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)|字符串|  
|real|REAL|float|  
|smalldatetime|TIMESTAMP|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|text|LONGVARCHAR|字符串|  
|time|TIME (1)|java.sql.Time (1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|字符串|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|字符串|  
|varchar(max)|VARCHAR|字符串|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|字符串<br /><br /> SQLXML|  
|sqlvariant|SQLVARIANT|对象|  
  
 （1） 到的时间使用 java.sql.Time[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]类型，必须设置**sendTimeAsDatetime**连接属性设置为 false。  
  
 （2） 你可以以编程方式访问的值**datetimeoffset**与[DateTimeOffset 类](../../connect/jdbc/reference/datetimeoffset-class.md)。  
  
 以下几部分提供了如何使用 JDBC 驱动程序和基本数据类型的实例。 有关如何在 Java 应用程序中使用的基本数据类型的更多详细示例，请参阅[基本数据类型示例](../../connect/jdbc/basic-data-types-sample.md)。  
  
## <a name="retrieving-data-as-a-string"></a>以字符串的格式检索数据  
 如果您必须从映射到任何以字符串形式查看的 JDBC 基本数据类型的数据源检索数据，或如果不需要强类型化的数据，则可以使用[getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类，如以下所示：  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>按数据类型检索数据  
 如果你需要从数据源，检索数据，并且您知道正在检索的数据的类型，使用其中一个 get\<类型 > SQLServerResultSet 方法类，也称为*getter 方法*。 可以使用 get 中使用的一个列名称或列索引\<类型 > 方法，如以下所示：  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  GetUnicodeStream 和使用扩展方法的 getBigDecimal 不推荐使用和不支持 JDBC 驱动程序。  
  
## <a name="updating-data-by-data-type"></a>按数据类型更新数据  
 如果你必须更新数据源中的字段的值，使用更新之一\<类型 > SQLServerResultSet 类的方法。 在下面的示例中， [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)结合使用方法[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法来更新数据源中的数据：  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  JDBC Driver 无法更新列名长度超过 127 个字符的 SQL Server 列。 如果尝试更新名称长度超过 127 个字符的列，将引发异常。  
  
## <a name="updating-data-by-parameterized-query"></a>通过参数化查询来更新数据  
 如果必须通过使用参数化的查询来更新数据源中的数据，你可以通过使用一组设置的参数的数据类型\<类型 > 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类，也称为*setter 方法*。 在下面的示例中， [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)方法用于预编译参数化的查询，然后[setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)方法用于设置之前参数的字符串值[executeUpdate](../../connect/jdbc/reference/executeupdate-method.md)调用方法。  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 有关参数化查询的详细信息，请参阅[SQL 语句中使用参数](../../connect/jdbc/using-an-sql-statement-with-parameters.md)。  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>向存储过程传递参数  
 如果你需要将类型化的参数传递到存储过程，你可以通过使用一组设置的参数按索引或名称\<类型 > 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。 在下面的示例中， [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法用于设置对存储过程的调用，然后[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)方法用于设置之前调用的参数[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)调用方法。  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  在此实例中，将返回一个结果集，包含此存储过程的运行结果。  
  
 有关使用存储的过程和输入的参数的 JDBC 驱动程序的详细信息，请参阅[使用输入参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)。  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>从存储过程检索参数  
 如果您必须检索和存储过程的参数，则必须首先注册输出参数按名称或索引使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 类并然后将指定的方法out 参数到相应的变量后返回运行存储过程调用。 在下面的示例中，prepareCall 方法用于设置对存储过程的调用，registerOutParameter 方法用于设置输出的参数，然后[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)方法用于设置的参数调用之前调用 executeQuery 方法。 通过存储过程的输出参数返回的值通过使用[getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)方法。  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  除返回的输出参数外，还可能返回一个结果集，包含此存储过程的运行结果。  
  
 有关如何使用 JDBC 驱动程序使用存储的过程和输出参数的详细信息，请参阅[使用输出参数的存储过程](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
