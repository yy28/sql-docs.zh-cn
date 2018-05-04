---
title: getPooledConnection 方法 （java.lang.String，java.lang.String） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 424ac4951ce4fd6f63644a154d7fd572dd5657be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>getPooledConnection 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  基于给定的用户名和密码尝试建立可用作池连接的物理数据库连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parameters  
 *user*  
  
 A**字符串**包含的用户名称。  
  
 *passwword*  
  
 A**字符串**包含的密码。  
  
## <a name="return-value"></a>返回值  
 A [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)对象。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>注释  
 由 javax.sql.ConnectionPoolDataSource 接口中的 getPooledConnection 方法指定此 getPooledConnection 方法。  
  
## <a name="see-also"></a>另请参阅  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成员](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 类](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
