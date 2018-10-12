---
title: getConnection 方法 (SQLServerPooledConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.getConnection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 05bdb61f-26e8-480f-a1c1-1e46a8ed4b70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 590fca2fcf97929755faa3633b257849b3fd7030
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687416"
---
# <a name="getconnection-method-sqlserverpooledconnection"></a>getConnection 方法 (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为此 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 对象表示的物理连接创建对象句柄。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>返回值  
 一个 Connection 对象。  
  
## <a name="exceptions"></a>异常  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 此 getConnection 方法由 javax.sql.PooledConnection 接口中的 getConnection 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成员](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 类](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
