---
title: JDBC 驱动程序 API 参考 |Microsoft Docs
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f311458a8fb6b58f22a1ca4c23fa8d1f36dddc51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773785"
---
# <a name="jdbc-driver-api-reference"></a>JDBC 驱动程序 API 参考

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供可在 Java 编程代码内使用的 API，并与 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库交互。



### <a name="javadocio-website-is-primary"></a>JavaDoc.io 网站是主数据库

为你查看 JavaDoc.io 网站上托管的 Microsoft JDBC API 参考文档。 JavaDoc.io 现在是我们有关 JDBC 参考文档的主网站。 JavaDoc.io 我们 JDBC 参考文档位于以下直接链接：

- [https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/](https://javadoc.io/doc/com.microsoft.sqlserver/mssql-jdbc/)

JavaDoc.io 已从版本 6.0 开始我们 JDBC 参考文档。

#### <a name="only-legacy-jdbc-documentation-is-here-on-docs"></a>仅旧版 JDBC 文档就在文档上

JDBC API 参考文档上的以下文章**https://docs.microsoft.com/sql/connect/jdbc/reference/** JDBC 类更新为新版本时将不再更新。 但是，此处的文章包含 JDBC 4.1 和 4.2 的版本的所有引用。

JDBC 版本 6.0 和某些更高版本中，文档也是此处。 但对于任何版本 6.0 或更高版本，请使用 JavaDoc.io 网站。



### <a name="important-notes"></a>重要说明

> [!NOTE]  
>  有关使用 JDBC 驱动程序的概念信息，请参阅[JDBC 驱动程序概述](../../../connect/jdbc/overview-of-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  对于 JDBC 4.1 和 4.2 符合性支持，请使用 Microsoft JDBC Driver 4.2 for SQL Server（或更高版本）。 以前版本的 Microsoft JDBC Drivers 4.1 和 4.0 不支持 JDBC 4.1 或 4.2 中引入的新方法。  
>   
>  本节内容不含有用于 JDBC 4.1 法规遵从性的 API 详细信息。 请参阅 [JDBC Driver 的 JDBC 4.1 符合性](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)。  
>   
>  本部分内容不含有 JDBC 4.2 合规性的 API 详细信息。 请参阅 [JDBC Driver 的 JDBC 4.2 符合性](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
>   
>  本部分内容不含有从 Microsoft JDBC Driver 4.2 for SQL Server 开始提供的大容量复制的 API 详细信息。 请参阅[通过 JDBC 驱动程序使用大容量复制](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
>   
>  本部分内容不含有从 Microsoft JDBC Driver 6.0 for SQL Server 开始提供的 Always Encrypted 的 API 详细信息。 请参阅 [JDBC 驱动程序的 Always Encrypted API 参考](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  在本部分中未找到 Using Table-Valued 参数，可从 Microsoft JDBC Driver 6.0 for SQL Server 开始的 API 详细信息。 请参阅[使用表值参数](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC Driver 6.4 支持使用 JDK 7.0、8.0 和 9.0 进行编译。  
>   
>  Microsoft JDBC Driver 6.2 支持使用 JDK 7.0 和 8.0 进行编译。  
>   
>  Microsoft JDBC Drivers 6.0 和 4.2 支持使用 JDK 5.0、6.0、7.0 和 8.0 进行编译。  
>   
>  Microsoft JDBC Driver 4.1 支持使用 JDK 5.0、6.0 和 7.0 进行编译。  



## <a name="interfaces"></a>界面  
  
|接口名称|描述|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 接口](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|允许你指定要与输入和输出参数一起使用的要调用的存储过程名称。|  
|[ISQLServerConnection 接口](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|表示连接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的 JDBC 连接。|  
|[SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|表示特定于使用 [ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的属性列表。|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|表示 JDBC 预定义语句功能的基本实现。|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|表示 JDBC 结果集。|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|表示 JDBC 语句功能的基本实现。|
| &nbsp; | &nbsp; |


  
## <a name="classes"></a>类  
  
|类名|描述|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|表示 microsoft.sql.DateTimeOffset 类型的对象。|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|表示二进制大型对象 (BLOB)。|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|实现 ISQLServerCallableStatement。|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|表示字符型二进制大型对象 (CLOB)。|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|实现 ISQLServerConnection。|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|表示用于连接池管理器的物理数据库连接。|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|表示数据库的元数据。|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|表示特定于使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的属性的列表。|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|表示将来自 Java 命名和目录接口 (JNDI) 的数据源具体化的对象工厂。|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|表示 JDBC 驱动程序。 此类包括连接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的方法以及取得 JDBC 驱动程序相关信息的方法。|  
|[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)|表示 SQL 语句运行不成功或不完整。|  
|[SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)|使用区域字符集表示字符型二进制大型对象。|  
|[SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)|表示用于预定义语句参数的元数据。|  
|[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)|表示连接池中的物理数据库连接。|  
|[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)|实现 ISQLServerPreparedStatement。|  
|[SQLServerResource](../../../connect/jdbc/reference/sqlserverresource-class.md)|表示本地化错误字符串资源。 此类仅计划供内部使用。|  
|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)|实现 ISQLServerResultSet。|  
|[SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)|表示结果集内包含的列的元数据。|  
|[SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md)|表示事务可回滚到的检查点。|  
|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)|实现 ISQLServerStatement。|  
|[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)|表示可参与分布式 (XA) 事务的 JDBC 连接。|  
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|表示在内部使用的 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 的对象工厂。|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|表示用于 XA 分布式事务管理的 XAResource。|
| &nbsp; | &nbsp; |



## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../../connect/jdbc/overview-of-the-jdbc-driver.md)

