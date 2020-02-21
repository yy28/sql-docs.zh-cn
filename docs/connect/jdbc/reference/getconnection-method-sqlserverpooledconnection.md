---
title: getConnection 方法 (SQLServerPooledConnection) | Microsoft Docs
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
ms.openlocfilehash: 352d867e444158cb2b8754a9cce1752bc4c2ee4a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67952692"
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
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>备注  
 此 getConnection 方法是由 javax.sql.PooledConnection 接口中的 getConnection 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成员](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 类](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
