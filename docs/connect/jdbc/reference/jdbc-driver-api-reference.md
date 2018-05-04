---
title: JDBC 驱动程序 API 参考 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4e1ae9d-18a6-41db-8bd2-9cf0eee4cccb
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a004657257c1b8695902fdab33ae2e4f7ec010dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="jdbc-driver-api-reference"></a>JDBC 驱动程序 API 参考
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供一个 API，可以在 Java 中使用编程代码连接到并与之交互[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。  
  
> [!NOTE]  
>  有关使用 JDBC 驱动程序的概念信息，请参阅[JDBC 驱动程序概述](../../../connect/jdbc/overview-of-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  有关 JDBC 4.1 和 4.2 法规遵从性支持，使用 Microsoft JDBC Driver 4.2 （或更高版本） for SQL Server。 以前版本的 Microsoft JDBC Drivers 4.1 和 4.0 不支持 JDBC 4.1 或 4.2 中引入的新方法。  
>   
>  本节内容不含有用于 JDBC 4.1 法规遵从性的 API 详细信息。 请参阅[JDBC 4.1 JDBC 驱动程序的符合性](../../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)。  
>   
>  本部分内容不含有 JDBC 4.2 合规性的 API 详细信息。 请参阅[JDBC 4.2 法规遵从性的 JDBC 驱动程序](../../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
>   
>  在本部分中未找到 API 用于大容量复制，可以开始与 Microsoft JDBC Driver 4.2 for SQL Server 的详细信息。 请参阅[使用 JDBC 驱动程序的大容量复制](../../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
>   
>  在本部分中未找到的始终加密，从 SQL Server 的 Microsoft JDBC Driver 6.0 开始提供的 API 详细信息。 请参阅[始终加密的 JDBC 驱动程序的 API 参考](../../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  
>   
>  在本部分中未找到 API 对于 Using Table-Valued 参数，从 SQL Server 的 Microsoft JDBC Driver 6.0 开始提供的详细信息。 请参阅[使用表值参数](../../../connect/jdbc/using-table-valued-parameters.md)  
>   
>  Microsoft JDBC 驱动程序 6.4 支持使用 JDK 7.0、 8.0 和 9.0 编译。  
>   
>  Microsoft JDBC 驱动程序 6.2 支持使用 JDK 7.0 和 8.0 编译。  
>   
>  Microsoft JDBC 驱动程序 6.0，然后使用 JDK 5.0、 6.0、 7.0 和 8.0 4.2 支持编译。  
>   
>  Microsoft JDBC Driver 4.1 支持使用 JDK 5.0、6.0 和 7.0 进行编译。  

## <a name="interfaces"></a>界面  
  
|接口名称|Description|  
|--------------------|-----------------|  
|[ISQLServerCallableStatement 接口](../../../connect/jdbc/reference/isqlservercallablestatement-interface.md)|允许你指定要与输入和输出参数一起使用的要调用的存储过程名称。|  
|[ISQLServerConnection 接口](../../../connect/jdbc/reference/isqlserverconnection-interface.md)|表示与的 JDBC 连接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库。|  
|[SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)|表示连接到的特定属性的列表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]通过使用数据库[ISQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)|表示 JDBC 预定义语句功能的基本实现。|  
|[ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)|表示 JDBC 结果集。|  
|[ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)|表示 JDBC 语句功能的基本实现。|  
  
## <a name="classes"></a>类  
  
|类名|Description|  
|----------------|-----------------|  
|[DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)|表示 microsoft.sql.DateTimeOffset 类型的对象。|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)|表示二进制大型对象 (BLOB)。|  
|[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)|实现 ISQLServerCallableStatement。|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)|表示字符型二进制大型对象 (CLOB)。|  
|[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)|实现 ISQLServerConnection。|  
|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)|表示用于连接池管理器的物理数据库连接。|  
|[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)|表示数据库的元数据。|  
|[SQLServerDataSource](../../../connect/jdbc/reference/isqlserverdatasource-interface.md)|表示连接到的特定属性的列表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]通过使用数据库[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)对象。|  
|[SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)|表示将来自 Java 命名和目录接口 (JNDI) 的数据源具体化的对象工厂。|  
|[SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)|表示 JDBC 驱动程序。 此类包括用于连接到的方法[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据库，并获取有关 JDBC 驱动程序信息。|  
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
|[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)|表示一个工厂[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)内部使用的对象。|  
|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)|表示为 XA XAResource 分布式事务管理。|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
