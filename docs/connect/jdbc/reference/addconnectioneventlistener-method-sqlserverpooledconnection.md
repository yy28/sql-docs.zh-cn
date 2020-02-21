---
title: addConnectionEventListener 方法 (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1377e29329f43b9ea982f168e394537295ec889
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67955964"
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>addConnectionEventListener 方法 (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  注册给定的事件侦听器，以便在此 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 对象发生事件时通知该侦听器。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>parameters  
 *listener*  
  
 ConnectionEventListener 对象。  
  
## <a name="remarks"></a>备注  
 此 addConnectionEventListener 方法是由 javax.sql.PooledConnection 接口中的 addConnectionEventListener 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成员](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 类](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
