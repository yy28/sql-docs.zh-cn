---
title: "SQLServerXAConnection 成员 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b61dabd-369b-460c-8450-9fe424f76541
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0303bdf87283f2a7fba87b58991239f5d92a10d7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaconnection-members"></a>SQLServerXAConnection 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
 无。  
  
## <a name="inherited-fields"></a>继承的字段  
 无。  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[addConnectionEventListener](../../../connect/jdbc/reference/addconnectioneventlistener-method-sqlserverpooledconnection.md)|(继承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 注册给定的事件侦听器，以便它在此连接对象上发生事件时将收到通知。|  
|[关闭](../../../connect/jdbc/reference/close-method-sqlserverpooledconnection.md)|(继承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 关闭此连接对象表示的物理连接。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverpooledconnection.md)|(继承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 创建此连接对象表示的物理连接对象句柄。|  
|[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)|检索[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)对象事务管理器将用来管理此参与[SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)在分布式事务中的对象。|  
|[removeConnectionEventListener](../../../connect/jdbc/reference/removeconnectioneventlistener-method-sqlserverpooledconnection.md)|(继承自[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)) 中删除给定的事件侦听器。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPooledConnection|addConnectionEventListener、close、getConnection、removeConnectionEventListener|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
|javax.sql.PooledConnection|addConnectionEventListener、close、getConnection、removeConnectionEventListener|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 类](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
