---
title: 使用连接池 |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d02cbb380d67b97dda38d262d3e942e19950b7a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-pooling"></a>使用连接池
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持 Java 平台企业版 (Java EE) 连接池。 JDBC Driver 实现了 JDBC 3.0 所需的接口，从而该驱动程序可参与任何中间件供应商提供的与 JDBC 3.0 兼容的连接池实现。 中间件（例如 Java EE 应用程序服务器）通常提供兼容的连接池工具。 JDBC 驱动程序将参与这些环境中的已池化的连接。  
  
> [!NOTE]  
>  尽管 JDBC 驱动程序支持 Java EE 5 连接池，但其自身并不提供池实现。 驱动程序依赖于第三方 Java 应用程序服务器来管理连接。  
  
## <a name="remarks"></a>注释  
 用于连接池实现的类如下。  
  
|类|实现|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc。 SQLServerXADataSource|javax.sql.ConnectionPoolDataSource 和 javax.sql.XADataSource|我们建议你使用[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)类为你的所有 Java EE 服务器需要因为它可以实现所有 JDBC 3.0 池和 XA 接口。|  
|com.microsoft.sqlserver.jdbc。 SQLServerConnectionPoolDataSource|javax.sql.ConnectionPoolDataSource|该类是一个连接工厂，它使得 Java EE 应用程序服务器可使用物理连接来填充它的连接池。 如果你的 Java EE 供应商的配置要求实现 javax.sql.ConnectionPoolDataSource 的类，将类名称指定为[SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)。 通常，我们建议你使用[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)类，因为它可实现这两个池和 XA 接口，并已验证在多个 Java EE 服务器配置。|  
  
 JDBC 应用程序代码应始终显式地关闭连接，以便从池中获得最大利益。 如果应用程序显式地关闭连接，则池实现可立即重新使用此连接。 如果连接未关闭，则其他应用程序无法重新使用它。 应用程序可以使用`finally`构造来确保即使发生异常时，关闭入池的连接。  
  
> [!NOTE]  
>  JDBC 驱动程序在将连接返回池中时，不会立即调用 sp_reset_connection 存储过程。 但是，驱动程序将依靠第三方 Java 应用程序服务器使连接返回其原始状态。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
