---
title: JDBC 驱动程序的 JDBC 4.1 合规性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f087fd40-8451-478e-b465-43112c711515
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea3d783fb98d22b3937016c9e6e60ed625ffca2d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027973"
---
# <a name="jdbc-41-compliance-for-the-jdbc-driver"></a>JDBC 驱动程序的 JDBC 4.1 合规性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  早于 Microsoft JDBC Driver 4.2 for SQL Server 的版本兼容 Java Database Connectivity API 4.0 规范。 本部分不适用于 4.2 版本之前的版本。  
  
 Microsoft JDBC Driver 4.2 for SQL Server 支持 Java Database Connectivity API 4.1 规范，并带有以下 API 方法。  
  
 **SQLServerConnection 类**  
  
|新方法|说明|JDBC 驱动程序实现|  
|----------------|-----------------|--------------------------------|  
|void abort(Executor executor)|终止 SQL Server 的打开连接。|按 java.sql.Connection 接口中所述实现。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)。|  
|void setSchema(String schema)|设置当前连接的架构。|SQL Server 不支持对当前会话设置架构。 如果调用此方法，该驱动程序将以无提示方式记录一条警告消息。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)。|  
|String getSchema()|返回当前连接的架构名称。|因为 SQL Server 不支持对当前连接设置架构，所以该驱动程序将改为返回用户的默认架构。 有关详细信息，请参阅 [java.sql.Connection](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)。|  
  
 **SQLServerDatabaseMetaData 类**  
  
|新方法|说明|JDBC 驱动程序实现|  
|----------------|-----------------|--------------------------------|  
|boolean generatedKeyAlwaysReturned()|当该驱动程序支持检索生成的键时，将返回 true|按 java.sql 中所述实现。 DatabaseMetaData 接口。 有关详细信息，请参阅 [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)。|  
|ResultSet getPseudoColumns(String catalog, String schemaPattern,String tableNamePattern,String columnNamePattern)|检索伪列/隐藏列的说明。|当 SQL Server 没有伪列的正式表示时，将返回一个空的结果集。 有关详细信息，请参阅 [java.sql.DatabaseMetaData](https://docs.oracle.com/javase/7/docs/api/java/sql/DatabaseMetaData.html)。|  
  
 **SQLServerStatement 类**  
  
|新方法|说明|JDBC 驱动程序实现|  
|----------------|-----------------|--------------------------------|  
|void closeOnCompletion()|指定在此语句依赖的所有结果集都关闭时关闭此语句。|按 java.sql.Statement 接口中所述实现。 有关详细信息，请参阅 [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)。|  
|boolean isCloseOnCompletion()|返回的值指示在此语句依赖的所有结果集都关闭时是否关闭此语句。|按 java.sql.Statement 接口中所述实现。 有关详细信息，请参阅 [java.sql.Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)。|  
  
 Microsoft JDBC Driver 4.2 for SQL Server 支持 Java Database Connectivity API 4.1 规范，并带有以下功能。  
  
|新功能|说明|  
|-----------------|-----------------|  
|新的转义函数<br /><br /> 限制返回行转义|部分支持<br /><br /> 转义语法：LIMIT \<rows> [OFFSET <row_offset>](using-sql-escape-sequences.md).|  
  
 Microsoft JDBC Driver 4.2 for SQL Server 支持 Java Database Connectivity API 4.1 规范，并带有以下数据类型映射。  
  
|数据类型映射|说明|  
|------------------------|-----------------|  
|PreparedStatement.setObject() 方法和 PreparedStatement.setNull() 方法现在支持新的数据类型映射。|1.新的 Java 到 JDBC 类型映射<br /><br /> (a) java.math.BigInteger 映射到 JDBC BIGINT<br /><br /> (b) java.util.Date 和 java.util.Calendar 映射到 JDBC TIMESTAMP<br /><br /> 2.新的数据类型转换：<br /><br /> (a) java.math.BigInteger 转换为 CHAR、VARCHAR、LONGVARCHAR 和 BIGINT<br /><br /> (b) java.util.Date and java.util.Calendar 转换为 CHAR、VARCHAR、LONGVARCHAR、DATE、TIME 和 TIMESTAMP<br /><br /> 有关详细信息，请参阅 JDBC 4.1 规范。|  
  
  
