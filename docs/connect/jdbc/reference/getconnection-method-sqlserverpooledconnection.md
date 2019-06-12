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
manager: jroth
ms.openlocfilehash: 1f1f42623344ddd4659df3d6163a9e8b89d6ae7b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66763198"
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
  
  
