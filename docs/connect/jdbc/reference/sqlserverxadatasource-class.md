---
title: SQLServerXADataSource 类 |Microsoft 文档
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
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7745863cfa6ad05d5aefa85b865751fe3f11f392
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 类
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示一个工厂[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)内部使用的对象。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **实现：** javax.sql.XADataSource  
  
## <a name="syntax"></a>语法  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>注释  
 通常，实现 SQLServerXADataSource 接口的对象已注册到使用 Java 命名和目录接口 (JNDI) 的命名服务。  
  
 SQLServerXADataSource 类提供了在分布式 (XA) 事务中使用的数据库连接。 SQLServerXADataSource 类还支持连接池的物理连接。 由实现 SQLServerXADataSource 和 SQLServerXAConnection 接口，在包 javax.sql 中定义， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
 SQLServerXAConnection 对象是可以参与分布式事务已入池的连接。 更确切地说，SQLServerXAConnection 通过添加方法来扩展 SQLServerPooledConnection 接口[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)。 此方法产生[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)事务管理器可以用于协调分布式事务中的其他参与者具有此连接上完成的工作的对象。 由于它们扩展 SQLServerPooledConnection 接口，SQLServerXAConnection 对象支持 SQLServerPooledConnection 对象的所有的方法。 它们是可重用的基础数据源物理连接，并且可生成可传递回 JDBC 应用程序的逻辑连接句柄。  
  
 SQLServerXAConnection 对象生成的 SQLServerXADataSource 对象。 SQLServerConnectionPoolDataSource 对象和 SQLServerXADataSource 对象是类似，因为它们并同时实现以下数据源层对 JDBC 应用程序可见。 此体系结构允许[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持分布式的事务中对应用程序是透明的方式。 SQLServerXADataSource 可以配置为与集成[!INCLUDE[msCoName](../../../includes/msconame_md.md)]分布式事务处理协调器 (DTC) 以提供 true，分布式事务处理。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXADataSource 成员](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
