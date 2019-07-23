---
title: 使用连接池 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 699d4e8a-34bf-4c60-b0d5-4a10dad6084a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec9d1717d12624ffa7663479f1d98146aea1137f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916335"
---
# <a name="using-connection-pooling"></a>使用连接池

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供对 Java 平台 Enterprise Edition (Java EE) 连接池的支持。 JDBC Driver 实现了 JDBC 3.0 所需的接口，从而该驱动程序可参与任何中间件供应商提供的与 JDBC 3.0 兼容的连接池实现。 中间件（例如 Java EE 应用程序服务器）通常提供兼容的连接池工具。 JDBC 驱动程序将参与这些环境中的已池化的连接。  
  
> [!NOTE]  
> 尽管 JDBC 驱动程序支持 Java EE 5 连接池，但其自身并不提供池实现。 驱动程序依赖于第三方 Java 应用程序服务器来管理连接。  
  
## <a name="remarks"></a>Remarks

用于连接池实现的类如下。  
  
| 类                                                           | 实现                                                    | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| com.microsoft.sqlserver.jdbc. SQLServerXADataSource             | javax.sql.ConnectionPoolDataSource 和 javax.sql.XADataSource | 建议对所有 Java EE 服务器需求都使用 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 类，因为它实现了所有的 JDBC 3.0 池和 XA 接口。                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| com.microsoft.sqlserver.jdbc. SQLServerConnectionPoolDataSource | javax.sql.ConnectionPoolDataSource                            | 该类是一个连接工厂，它使得 Java EE 应用程序服务器可使用物理连接来填充它的连接池。 如果 Java EE 供应商的配置需要实现 javax.sql.ConnectionPoolDataSource 的类，则将该类的名称指定为 [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)。 通常，建议改用 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 类，因为它同时实现了池和 XA 接口，并且已在更多的 Java EE 服务器配置中经过了验证。 |
  
 JDBC 应用程序代码应始终显式地关闭连接，以便从池中获得最大利益。 如果应用程序显式地关闭连接，则池实现可立即重新使用此连接。 如果连接未关闭，则其他应用程序无法重新使用它。 应用程序可使用 `finally` 构造来确保关闭已池化的连接，即使发生异常。  
  
> [!NOTE]  
> JDBC 驱动程序在将连接返回池中时，不会立即调用 sp_reset_connection 存储过程。 但是，驱动程序将依靠第三方 Java 应用程序服务器使连接返回其原始状态。  
  
## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
