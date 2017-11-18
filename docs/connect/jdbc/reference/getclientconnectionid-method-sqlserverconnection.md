---
title: "getClientConnectionID 方法 (SQLServerConnection) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bee39c11-733a-461f-92cc-33efcb2af87d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b422c085307db5630cb1b70a47cafd935877dcd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getclientconnectionid-method-sqlserverconnection"></a>getClientConnectionID 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  无论最新连接尝试成功还是失败，都获取该尝试的连接 ID。  
  
## <a name="syntax"></a>语法  
  
```vb  
public Java.util.UUID SQLServerConnection.getClientConnectionID();  
```  
  
## <a name="return-value"></a>返回值  
 表示最新连接尝试的连接 ID 的 16 字节的 GUID。 或者为 NULL（如果在启动连接请求和预登录握手后失败）。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 有关访问扩展的事件日志中的诊断信息的详细信息，请参阅[访问扩展的事件日志中的诊断信息](../../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
 以下示例显示如何获取连接 ID：  
  
```  
Connection con = DriverManager.getConnection(connectionUrl);  
UUID id = ((ISQLServerConnection)con).getClientConnectionId();  
```  
  
 以下示例显示获取连接 ID 的另一种方法：  
  
```  
SQLServerConnectionPoolDataSource ds = new SQLServerConnectionPoolDataSource();  
ds.setUser("…");  
ds.setPassword("…");  
ds.setServerName("…");  
PooledConnection pcon= ds.getPooledConnection();  
Connection cn = pcon.getConnection();  
UUID conid = ((ISQLServerConnection)cn).getClientConnectionId();  
```  
  
 **getClientConnectionID**无论哪个版本的服务器的工作原理你连接到，但扩展的事件日志和上连接环形缓冲区错误项将不会显示在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]2008 R2 及更早版本。  
  
 如果启用记录连接 ID 的扩展事件，您可以在扩展事件日志中查找连接 ID，以查看失败是否源自服务器。 你还可以连接环形缓冲区中找到的连接 ID ([连接中使用连接环形缓冲区的 SQL Server 2008 的故障排除](http://go.microsoft.com/fwlink/?LinkId=207752)) 对于某些连接错误。 如果在连接环形缓冲区中找不到连接 ID，可以认为是网络错误。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

