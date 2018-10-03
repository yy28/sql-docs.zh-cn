---
title: 使用自适应缓冲 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 92d4e3be-c3e9-4732-9a60-b57f4d0f7cb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16ac54c78839df4c5ce911a1258dfa052ac1666c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624997"
---
# <a name="using-adaptive-buffering"></a>使用自适应缓冲

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

自适应缓冲的作用是在无需服务器游标开销的情况下检索任何类型的大值数据。 应用程序可以在受驱动程序支持的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中使用自适应缓冲功能。

通常，当 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 执行查询时，驱动程序会将服务器中的所有结果检索到应用程序内存中。 尽管这种方法可以最大程度地减少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的资源占用，但它可能会在 JDBC 应用程序中针对生成非常大的结果的查询引发 OutOfMemoryError。

为了使应用程序可以处理非常大的结果，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供了自适应缓冲。 借助于自适应缓冲，驱动程序可以在应用程序需要时从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中检索语句执行结果，而不是一次性检索全部结果。 一旦应用程序不再访问结果，驱动程序还会立即丢弃它们。 以下是可以使用自适应缓冲的一些示例：

- 查询生成非常大的结果集：应用程序可能执行一个 SELECT 语句，此语句生成的行数超过了应用程序可在内存中存储的行数。 在先前的版本中，应用程序必须使用服务器游标才能避免 OutOfMemoryError。 借助于自适应缓冲，可以对任意大的结果集执行只进只读传递，而不需要服务器游标。

- 查询生成非常大的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 列或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) OUT 参数值：应用程序可能检索单个值（列或 OUT 参数），而该值太大，无法全部放入应用程序内存中。 自适应缓冲允许客户端应用程序使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法检索此类值作为流。 当应用程序从流中读取数据时，将从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中检索值。

> [!NOTE]  
> 使用自适应缓冲时，JDBC Driver 只会缓冲它必须缓冲的那些数据。 该驱动程序未提供任何公共方法来控制或限制缓冲区的大小。

## <a name="setting-adaptive-buffering"></a>设置自适应缓冲

从 JDBC Driver 2.0 版起，该驱动程序的默认行为就是“adaptive”。 换言之，要获取自适应缓冲行为，应用程序不必显式请求自适应行为。 不过，在 1.2 版中，缓冲模式默认为“full”，并且应用程序必须显式请求自适应缓冲模式。

应用程序可以通过三种方法请求语句执行应使用自适应缓冲：

- 应用程序可以设置连接属性**responseBuffering**为"adaptive"。 有关设置连接属性的详细信息，请参阅[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)。

- 应用程序可以使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md) 方法为通过该 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 对象创建的所有连接设置响应缓冲模式。

- 应用程序可以使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法为特定的语句对象设置响应缓冲模式。

使用 JDBC Driver 1.2 时，应用程序需要将语句对象强制转换为 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 类才能使用 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法。 中的代码示例[读取大型数据样本](../../connect/jdbc/reading-large-data-sample.md)并[读取大数据与存储过程示例](../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)说明了这种旧的用法。

但是，使用 JDBC Driver 2.0 时，应用程序无需关于实现类层次结构的任何假设，即可使用 [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) 方法和 [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 方法来访问供应商特定的功能。 有关示例代码，请参阅[更新大型数据样本](../../connect/jdbc/updating-large-data-sample.md)主题。

## <a name="retrieving-large-data-with-adaptive-buffering"></a>使用自适应缓冲检索大型数据

当使用 get\<Type>Stream 方法一次性读取较大值，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 按返回的顺序访问 ResultSet 列和 CallableStatement OUT 参数时，自适应缓冲在处理结果时可以最大程度地减少使用的应用程序内存。 使用自适应缓冲时：

- 在 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类中定义的 get\<Type>Stream 方法默认情况下返回只读取一次的流，尽管可以重置流（如果应用程序已进行标记）。 如果应用程序要对流执行 `reset`，它必须先对该流调用 `mark` 方法。

- 在 [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) 和 [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) 类中定义的 get\<Type>Stream 方法返回的流始终可以重定位至流的开始位置，而不必调用 `mark` 方法。

当应用程序使用自定义缓冲时，由 get\<Type>Stream 方法检索的值仅供检索一次。 如果在调用同一列或同一参数的 get\<Type>Stream 方法后，试图对同一对象调用任何 get\<Type> 方法，则将引发异常并显示消息“数据已访问，不可用于此列或此参数”。

> [!NOTE]
> 对 ResultSet.close() 了结果集处理过程的调用需要 Microsoft JDBC Driver for SQL Server 读取并丢弃其余的所有数据包。 如果查询返回了大型数据集，尤其是如果网络连接速度较慢，这可能需要大量的时间。

## <a name="guidelines-for-using-adaptive-buffering"></a>自适应缓冲使用准则

开发人员应遵循以下重要准则，以尽可能减少应用程序占用的内存：

- 应避免使用连接字符串属性 selectMethod=cursor 来允许应用程序处理非常大的结果集。 自适应缓冲功能允许应用程序在不使用服务器游标的情况下处理非常大的只进、只读结果集。 请注意，设置 selectMethod=cursor 时，该连接生成的所有只进只读结果集都会受到影响。 换言之，如果应用程序例行处理只有几行的短结果集，则与没有将 selectMethod 设置为 cursor 的情况相比，针对每个结果集创建、读取和关闭服务器游标在客户端和服务器端都会使用更多的资源。

- 通过使用 getAsciiStream、 getBinaryStream 或 getCharacterStream 方法而不 getBlob 或 getClob 方法，流的形式读取大文本或二进制值。 从版本 1.2 开始，[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类提供了新的 get\<Type>Stream 方法来实现此目的。

- 确保在 SELECT 语句中将可能具有大值的列放在列列表的最后，并且使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 的 get\<Type>Stream 方法按选择列时的顺序来访问这些列。

- 确保在用来创建 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 的 SQL 语句的参数列表中，最后声明可能具有大值的 OUT 参数。 此外，确保使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 的 get\<Type>Stream 方法，按照声明 OUT 参数时的顺序访问这些参数。

- 避免同时对同一连接执行一条以上的语句。 如果在处理上一条语句的结果之前执行另一条语句，可能导致将未处理的结果缓冲到应用程序内存中。

- 某些情况下使用**selectMethod = cursor**而不是**responseBuffering = adaptive**可能更有利，例如：

  - 如果应用程序处理只进、 只读结果集速度慢，例如，使用某些用户输入后, 再读取每一行**selectMethod = cursor**而不是**responseBuffering = adaptive**可能帮助减少使用的资源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

  - 如果应用程序在同一连接上同时处理两个或更多的只进只读结果集，则处理这些结果集时，使用 selectMethod=cursor（而不是 responseBuffering=adaptive）可能有助于减少驱动程序需要的内存。

  在这两种情况下，需要考虑创建、读取和关闭服务器游标的开销。

此外，下面的列表针对可滚动的结果集和只进的可更新结果集提供了一些建议：

- 对于可滚动结果集，在提取行块时，驱动程序始终会将 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 方法所指示的行数读入内存，即使在启用了自适应缓冲的情况下也是如此。 如果滚动导致 OutOfMemoryError，可以调用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法将提取大小设置为较少的行数（如果必要，甚至可减小到 1 行），从而减少提取的行数。 如果这样还是无法防止 OutOfMemoryError，则应避免在可滚动的结果集中包含非常大的列。

- 对于只进的可更新结果集，在提取行块时，驱动程序通常会将 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [getFetchSize](../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md) 方法所指示的行数读入内存，即使在该连接上启用了自适应缓冲的情况下也是如此。 如果调用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md) 方法导致 OutOfMemoryError，可以调用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法将提取大小设置为较少的行数（如果必要，甚至可减小到 1 行），从而减少提取的行数。 执行该语句前，也可以调用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法并提供参数“adaptive”来强制驱动程序不缓冲任何行。 因为该结果集是不可滚动的，所以如果应用程序使用 get\<Type>Stream 方法之一访问大型列值，驱动程序将会在应用程序读取该值后立即将其丢弃，正如对只进只读结果集所做的那样。

## <a name="see-also"></a>另请参阅

[借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
