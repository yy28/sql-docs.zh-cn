---
title: SQLServerXADataSource 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa85b61a67655fbf363c1927b48cd79f8ff841ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774415"
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示在内部使用的 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 的对象工厂。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：**[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **实现：** javax.sql.XADataSource  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>Remarks  
 实现 SQLServerXADataSource 接口的对象通常是在使用 Java 命名和目录接口 (JNDI) 的命名服务中注册的。  
  
 SQLServerXADataSource 类提供可在分布式 (XA) 事务中使用的数据库连接。 SQLServerXADataSource 类还支持物理连接的连接池。 SQLServerXADataSource 和 SQLServerXAConnection 接口，在包 javax.sql 中定义，由实现[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 SQLServerXAConnection 对象是可参与分布式事务的池连接。 SQLServerXAConnection 更准确地说，通过添加方法来扩展 SQLServerPooledConnection 接口[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)。 此方法生成 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象，事务管理器可使用此对象在此连接上所执行的操作与分布式事务中的其他参与者之间进行协调。 由于它们扩展 SQLServerPooledConnection 接口，SQLServerXAConnection 对象支持 SQLServerPooledConnection 对象的所有方法。 它们是可重用的基础数据源物理连接，并且可生成可传递回 JDBC 应用程序的逻辑连接句柄。  
  
 SQLServerXADataSource 对象生成 SQLServerXAConnection 的对象。 SQLServerConnectionPoolDataSource 对象和 SQLServerXADataSource 对象很相似，因为它们并同时实现对 JDBC 应用程序可见的数据源层之下。 此体系结构使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 能够以对应用程序透明的方式支持分布式事务。 SQLServerXADataSource 可以配置为与 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 分布式事务处理协调器 (DTC) 集成，以提供真正的分布式事务处理。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXADataSource 成员](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
