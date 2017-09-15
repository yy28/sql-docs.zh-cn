---
title: "了解 Java EE 支持 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b878069cb0ddf04d4c8c743795f876b00fef23dc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-java-ee-support"></a>了解 Java EE 支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  下面的部分文档如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]为 Java 平台、 Enterprise Edition (Java EE) 和 JDBC 3.0 可选 API 功能提供支持。 本“帮助”系统中提供的源代码示例提供了很好的参考资料，供你开始使用这些功能。  
  
 首先，确保您的 Java 环境（JDK、JRE）包含 javax.sql 包。 这是使用可选 API 的任何 JDBC 应用程序所必需的包。 JDK 1.5 和更高版本已包含此包，因此你不需要单独安装它。  
  
## <a name="driver-name"></a>驱动程序名称  
 驱动程序类名称是**com.microsoft.sqlserver.jdbc.SQLServerDriver**。 JDBC 驱动程序 4.0、 4.1、 4.2 和 6.0，该驱动程序包含在 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 文件中。 JDBC 驱动程序 6.2，有关该驱动程序包含在 mssql jdbc 6.2.1.jre7.jar 或 mssql jdbc 6.2.1.jre8.jar。
  
 每当加载与 JDBC 驱动程序管理器类驱动程序，则使用类名称。 另外，只要你在任何驱动程序配置中必须指定驱动程序的类名称，则也将用到它。 例如，配置 Java EE 应用程序服务器内的数据源可能要求您输入驱动程序类名称。  
  
## <a name="data-sources"></a>数据源  
 JDBC 驱动程序为 Java EE / JDBC 3.0 数据源提供支持。 JDBC 驱动程序[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)类实现由**com.microsoft.sqlserver.jdbc.SQLServerXADataSource**。  
  
### <a name="datasource-names"></a>数据源名称  
 可以使用数据源来建立数据库连接。 下表中描述了可用于 JDBC 驱动程序的数据源：  
  
|数据源类型|类名称和描述|  
|---------------|--------------------------|  
|DataSource|com.microsoft.sqlserver.jdbc.SQLServerDataSource <br/> <br/> 非连接池数据源。|  
|ConnectionPoolDataSource|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource <br/> <br/> 用于配置 JAVA EE 应用程序服务器连接池的数据源。 通常当应用程序在 JAVA EE 应用程序服务器中运行时使用。|  
|XADataSource|com.microsoft.sqlserver.jdbc.SQLServerXADataSource <br/> <br/> 用于配置 JAVA EE XA 数据源的数据源。 通常当应用程序在 JAVA EE 应用程序服务器和 XA 事务管理器中运行时使用。|  
  
### <a name="data-source-properties"></a>数据源属性  
 所有数据源均支持设置和获取与基础驱动程序的属性集关联的任何属性的功能。  
  
 示例：  
  
 `setServerName("localhost");`  
  
 `setDatabaseName("AdventureWorks");`  
  
 下面的内容说明应用程序如何使用数据源进行连接：  
  
```  
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 有关数据源属性的详细信息，请参阅[设置数据源属性](../../connect/jdbc/setting-the-data-source-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

