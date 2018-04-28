---
title: 使用自适应缓冲 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
caps.latest.revision: 53
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 194301cbaa751beedb3ba70bfb78bc6062b0841f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-adaptive-buffering"></a>使用自适应缓冲
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  自适应缓冲的作用是在无需服务器游标开销的情况下检索任何类型的大值数据。 应用程序可以使用自适应缓冲功能与所有版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]由驱动程序支持。  
  
 通常，当[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]执行查询，该驱动程序的所有结果从服务器中检索到应用程序内存。 尽管这种方法最大程度减少资源消耗上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，它可以引发 OutOfMemoryError JDBC 应用程序生成非常大的结果的查询中。  
  
 若要允许应用程序来处理非常大的结果，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供自适应缓冲。 使用自适应缓冲，驱动程序检索语句执行结果从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]随着应用程序需要它们，而不是一次。 一旦应用程序不再访问结果，驱动程序还会立即丢弃它们。 以下是可以使用自适应缓冲的一些示例：  
  
-   **此查询生成一个非常大型结果集：**应用程序可以执行生成不是应用程序可以在内存中存储的更多行的 SELECT 语句。 在以前版本中，应用程序必须使用服务器游标来避免发生内存不足错误。 借助于自适应缓冲，可以对任意大的结果集执行只进只读传递，而不需要服务器游标。  
  
-   **此查询生成非常大**[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)**列或**[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)**出参数值：**应用程序可以检索单个值 (列或 OUT 参数) 太大，无法完全纳入应用程序内存。         自适应缓冲允许客户端应用程序通过使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法检索作为流，这样的值。 应用程序检索的值从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如从流中读取。  
  
> [!NOTE]  
>  使用自适应缓冲时，JDBC Driver 只会缓冲它必须缓冲的那些数据。 该驱动程序未提供任何公共方法来控制或限制缓冲区的大小。  
  
## <a name="setting-adaptive-buffering"></a>设置自适应缓冲  
 从开始 JDBC 驱动程序版本 2.0 中，该驱动程序的默认行为是"**自适应**"。 换言之，要获取自适应缓冲行为，应用程序不必显式请求自适应行为。 在版本 1.2 版本中，但是，缓冲模式处于"**完整**"默认情况下和应用程序必须显式请求的自适应缓冲模式。  
  
 应用程序可以通过三种方法请求语句执行应使用自适应缓冲：  
  
-   应用程序可以将连接属性设置**responseBuffering**为"自适应"。 有关设置连接属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
-   应用程序可以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)对象以设置响应缓冲模式，通过创建的所有连接[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)对象。  
  
-   应用程序可以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类来设置响应缓冲模式的特定语句对象。  
  
 使用 JDBC 驱动程序版本 1.2，语句将对象转换为所需的应用程序时[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)类以使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法。 中的代码示例[读取大型数据示例](../../connect/jdbc/reading-large-data-sample.md)和[读取大型数据的存储过程示例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)演示此旧的用法。  
  
 但是，与 JDBC 驱动程序版本 2.0 中，应用程序可以使用[isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)方法和[unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)方法来访问有关的特定于供应商功能而无需任何假设实现类层次结构。 有关示例代码，请参阅[更新大型数据示例](../../connect/jdbc/updating-large-data-sample.md)主题。  
  
## <a name="retrieving-large-data-with-adaptive-buffering"></a>使用自适应缓冲检索大型数据  
 当较大的值读取一次通过使用 get\<类型 > 流方法和结果集列和 CallableStatement OUT 参数中返回的顺序访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，自适应缓冲最小化应用程序内存使用量时处理结果。 使用自适应缓冲时：  
  
-   Get\<类型 > 流中定义的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类在虽然可以重置流，如果默认情况下，返回读取一次流标记由应用程序。 如果想要将应用程序`reset`流，它必须调用`mark`方法的第一次流式处理。  
  
-   Get\<类型 > 流中定义的方法[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md)和[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md)类返回流始终可重新定位到而无需流的开始位置调用`mark`方法。  
  
 当应用程序使用自适应缓冲，通过 get 检索到的值\<类型 > 流方法只能检索一次。 如果你尝试调用任何 get\<类型 > 参数调用 get 后的在同一列上的方法\<类型 > 的同一个对象，异常流方法将引发与消息，"数据已被访问并不是可供此列或参数"。  
  
> [!NOTE]
> 对 ResultSet.close() 中间处理了结果集的调用将需要 Microsoft JDBC Driver for SQL Server 读取并放弃所做的剩余的所有数据包。 如果查询返回了大型数据集，特别是如果网络连接很慢，这可能需要大量的时间。     
  
## <a name="guidelines-for-using-adaptive-buffering"></a>自适应缓冲使用准则  
 开发人员应遵循以下重要准则，以尽可能减少应用程序占用的内存：  
  
-   避免使用连接字符串属性**selectMethod = 光标**若要允许应用程序处理非常大的结果设置。 自适应缓冲功能允许应用程序在不使用服务器游标的情况下处理非常大的只进、只读结果集。 请注意，当你设置**selectMethod = 光标**、 所有只进、 只读结果集由该连接都受到影响。 如果你的应用程序定期处理短结果集所包含的少量的行，换而言之，创建、 读取和关闭服务器游标，对于每个结果集将使用在客户端和服务器端上的资源不是这种情况其中**selectMethod**未设置为**光标**。  
  
-   通过使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法而不 getBlob 或 getClob 方法，流的形式读取大文本或二进制值。 从版本 1.2 发行版，开始[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类提供了新的 get\<类型 > 流式处理为此目的的方法。  
  
-   确保具有可能很大的值的列的 SELECT 语句中的列列表中上一次放置 get\<类型 > 流式传输的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)用于访问中的列选择它们的顺序。  
  
-   确保，OUT 参数可能很大的值与上次中声明的用于创建 SQL 中的参数列表[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)。 此外，确保 get\<类型 > 流式传输的方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)用于访问声明它们的顺序中的 OUT 参数。  
  
-   避免同时对同一连接执行一条以上的语句。 如果在处理上一条语句的结果之前执行另一条语句，可能导致将未处理的结果缓冲到应用程序内存中。  
  
-   在某些情况下，使用**selectMethod = 光标**而不是**responseBuffering = 自适应**很多有益，如：  
  
    -   如果你的应用程序处理只进、 只读结果设置缓慢，如后使用某些用户输入，读取每个行**selectMethod = 光标**而不是**responseBuffering = 自适应**可能帮助减少使用资源[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果你的应用程序处理两个或更只进、 只读结果集同时在同一连接上，使用**selectMethod = 光标**而不是**responseBuffering = 自适应**可能帮助减少驱动程序在处理这些结果集时所需的内存。  
  
     在这两种情况下，需要考虑创建、读取和关闭服务器游标的开销。  
  
 此外，下面的列表针对可滚动的结果集和只进的可更新结果集提供了一些建议：  
  
-   对于可滚动的结果集时始终提取块，这些行驱动程序读取到内存的指示的行数, [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象，即使启用自适应缓冲。 如果滚动导致 OutOfMemoryError，你可以减少通过调用提取的行数[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象将提取大小设置为较小的行数即使下一行，如有必要。 如果这不会阻止 OutOfMemoryError，避免在可滚动的结果集包括非常大的列。  
  
-   对于只进的可更新结果集，当提取块，这些行驱动程序通常读取到内存的指示的行数时[getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象，即使自适应缓冲是启用了时连接上。 如果调用[下一步](../../connect/jdbc/reference/next-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象会导致 OutOfMemoryError，你可以减少通过调用提取的行数[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象将提取大小设置为较小的行，即使下一行，如有必要。 您也可以强制驱动程序不通过调用缓冲的任何行[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象"**自适应**"之前的参数执行语句。 因为结果集不是可滚动的如果应用程序通过使用其中一个 get 访问大型列值\<类型 > 流方法驱动程序将丢弃值就会立即应用程序读取它的只进一样，它在只读的结果集。  
  
## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
