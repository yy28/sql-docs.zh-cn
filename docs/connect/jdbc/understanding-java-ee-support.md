---
title: 了解 Java EE 支持 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9448b80-b7a3-49cf-8bb4-322c73676005
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d5cc306a407e818a79d67cfc4c4340e1a9c2b22
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278858"
---
# <a name="understanding-java-ee-support"></a>了解 Java EE 支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  以下各部分介绍 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 如何为 Java Platform、Enterprise Edition (Java EE) 和 JDBC 3.0 可选 API 功能提供支持。 本“帮助”系统中提供的源代码示例提供了很好的参考资料，供你开始使用这些功能。  
  
 首先，确保您的 Java 环境（JDK、JRE）包含 javax.sql 包。 这是使用可选 API 的任何 JDBC 应用程序所必需的包。 JDK 1.5 和更高版本已包含此包，因此不需要单独安装它。  
  
## <a name="driver-name"></a>驱动程序名称  
 驱动程序类名称为 com.microsoft.sqlserver.jdbc.SQLServerDriver。 对于 JDBC 驱动程序 4.1、4.2 和 6.0，驱动程序包含在 sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 文件中。 对于 JDBC Driver 6.2，mssql jdbc 6.2.1.jre7.jar 或 mssql jdbc 6.2.1.jre8.jar 中包含驱动程序。 对于 JDBC Driver 6.4 mssql jdbc 6.4.0.jre7.jar、 mssql jdbc 6.4.0.jre8.jar 或 mssql jdbc 6.4.0.jre9.jar 中包含该驱动程序。
  
 只要使用 JDBC DriverManager 类加载驱动程序，就会使用此类名称。 另外，只要在任何驱动程序配置中必须指定驱动程序的类名称，则也将用到它。 例如，配置 Java EE 应用程序服务器内的数据源可能要求输入驱动程序类名称。  
  
## <a name="data-sources"></a>“数据源”  
 JDBC 驱动程序为 Java EE / JDBC 3.0 数据源提供支持。 JDBC 驱动程序 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 类是由 com.microsoft.sqlserver.jdbc.SQLServerXADataSource 实现的。  
  
### <a name="datasource-names"></a>数据源名称  
 可以使用数据源来建立数据库连接。 下表中描述了可用于 JDBC 驱动程序的数据源：  
  
|数据源类型|类名和说明|  
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
  
```java
initialize JNDI ..  
Context ctx = new InitialContext(System.getProperties());  
...  
DataSource ds = (DataSource) ctx.lookup("MyDataSource");  
Connection c = ds.getConnection("user", "pwd");  
```  
  
 有关数据源属性的详细信息，请参阅[设置数据源属性](../../connect/jdbc/setting-the-data-source-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
