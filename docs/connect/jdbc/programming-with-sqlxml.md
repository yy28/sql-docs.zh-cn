---
title: "使用 SQLXML 编程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5737ae7a0356f7697b254e67faa5cf715d2ffaef
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="programming-with-sqlxml"></a>使用 SQLXML 进行编程
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本部分介绍如何使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]API 方法来存储和检索 XML 文档中和从关系数据库与**SQLXML**对象。  
  
 本节还包含有关 SQLXML 对象类型的信息，并提供使用 SQLXML 对象的重要准则和限制的列表。  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>使用 SQLXML 对象读取和写入 XML 数据  
 以下列表介绍如何使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]API 方法来读取和写入与 SQLXML 对象的 XML 数据：  
  
-   若要创建 SQLXML 对象，请使用[createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 请注意，此方法创建的是无任何数据的 SQLXML 对象。 若要添加**xml**数据到 SQLXML 对象调用 SQLXML 接口中指定的以下方法之一： setResult，setCharacterStream，setBinaryStream，或 setString。  
  
-   若要检索 SQLXML 对象本身，使用的 getSQLXML 方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。  
  
-   若要检索**xml**数据从 SQLXML 对象，使用 SQLXML 接口中指定的以下方法之一： getSource，getCharacterStream，getBinaryStream，或 getString。  
  
-   若要更新**xml** SQLXML 对象中的数据使用[updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
-   若要将 SQLXML 对象存储在数据库表类型的列**xml**，使用的 setSQLXML 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类或[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。  
  
 中的代码示例[SQLXML 数据类型示例](../../connect/jdbc/sqlxml-data-type-sample.md)演示如何执行这些常见的 API 任务。  
  
## <a name="readable-and-writable-sqlxml-objects"></a>可读写的 SQLXML 对象  
 下表列出 JDBC API 提供的 setter、getter 和 updater 方法所支持的 SQLXML 对象类型。 表中的列引用以下内容：  
  
-   **方法名称**列列出 JDBC API 中支持的 getter 和 setter，更新程序方法。  
  
-   **Getter SQLXML 对象**列表示通过以下任一方法创建的 SQLXML 对象[getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类或[getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
-   **Setter SQLXML 对象**列表示 SQLXML 对象，由创建[createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)类。 请注意下面的 setter 方法接受由创建的 SQLXML 对象[createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)方法。  
  
|方法名称|Getter SQLXML 对象<br /><br /> （可读）|Setter SQLXML 对象<br /><br /> （可写）|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement.setSQLXML()|不支持|是否支持|  
|CallableStatement.setObject()|不支持|是否支持|  
|PreparedStatement.setSQLXML()|不支持|是否支持|  
|PreparedStatement.setObject()|不支持|是否支持|  
|ResultSet.updateSQLXML()|不支持|是否支持|  
|ResultSet.updateObject()|不支持|是否支持|  
|ResultSet.getSQLXML()|是否支持|不支持|  
|CallableStatement.getSQLXML()|是否支持|不支持|  
  
 如上表所示，setter SQLXML 方法将不会处理可读的 SQLXML 对象；同样，getter 方法将不会处理可写的 SQLXML 对象。  
  
 如果应用程序通过使用 SQLXML 对象指定小数位数或长度参数来调用 setObject 方法，将忽略该缩放或长度的参数。  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>使用 SQLXML 对象的指导原则和限制  
 应用程序可以使用 SQLXML 对象从/向数据库中读取/写入 XML 数据。 下面的列表提供了有关使用 SQLXML 对象时的具体限制和准则的信息：  
  
-   SQLXML 对象只能在创建它的事务的持续时间内保持有效。  
  
-   通过 getter 方法接收的 SQLXML 对象只能用于读取数据。  
  
-   通过连接对象创建的 SQLXML 对象只能用于写入数据。  
  
-   应用程序只能对可读的 SQLXML 对象调用一个 getter 方法来读取数据。 调用该 getter 方法后，对同一 SQLXML 对象调用其他所有 getter 或 setter 方法都将失败。  
  
-   读取或写入到后，应用程序可以调用仅 SQLXML 对象上的可用方法。 但是，只要基础列或参数处于活动状态，就仍然可以处理返回的流或源。 如果基础列或参数变为非活动状态，与 SQLXML 对象关联的流或源就会关闭。 如果基础列或参数不再有效，Stream、Simple API for XML (SAX) 和 Streaming API for XML (StAX) getter 将无法使用基础数据。  
  
-   应用程序只能对可写的 SQLXML 对象调用一个 setter 方法。 调用该 setter 方法后，对同一 SQLXML 对象调用其他所有 getter 或 setter 方法都将失败。  
  
-   要为 SQLXML 对象设置数据，应用程序必须在返回的对象中使用相应的 setter 方法和函数。  
  
-   GetSQLXML 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类和[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类返回**null**数据如果基础列是**null**。  
  
-   setter 对象可以在创建它们的连接期间内保持有效。  
  
-   不允许应用程序设置**null**通过使用 SQLXML 接口提供的 setter 方法的值。 应用程序可以使用 SQLXML 接口中提供的 setter 方法来设置空字符串 ("")。 若要设置**null**值，应用程序应调用以下项之一：  
  
    -   SetNull 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类和[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。  
  
    -   SetObject 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类和[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类。  
  
    -   SetSQLXML 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类和[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)类，该类具有**null**参数值。  
  
-   处理 XML 文档时，出于性能方面的考虑，建议使用 Simple API for XML (SAX) 和 Streaming API for XML (StAX) 分析器，而不要使用文档对象模型 (DOM) 分析器。  
  
 XML 分析器无法处理空值。 但是，SQL Server 允许应用程序在 XML 数据类型的数据库列中检索和存储空值。 这意味着，分析 XML 数据时，如果基础值为空，分析器将引发异常。 对于 DOM 输出，JDBC driver 会捕获该异常并引发错误。 对于 SAX 和 Stax 输出，此错误直接来自分析器。  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>自适应缓冲和 SQLXML 支持  
 SQLXML 对象返回的二进制流和字符流遵循自适应或完全缓冲模式。 另一方面，如果 XML 分析器不是流，则不会遵循自适应或完全设置。 有关自适应缓冲的详细信息，请参阅[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另请参阅  
 [支持 XML 数据](../../connect/jdbc/supporting-xml-data.md)  
  
  

