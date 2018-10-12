---
title: addConnectionEventListener 方法 (SQLServerPooledConnection) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7fbd278bfa95d0697d7435ccac132a60112b32d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799605"
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>addConnectionEventListener 方法 (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  注册给定的事件侦听器，以便在此 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 对象发生事件时通知该侦听器。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>Parameters  
 *listener*  
  
 一个 ConnectionEventListener 对象。  
  
## <a name="remarks"></a>Remarks  
 此 addConnectionEventListener 方法由 javax.sql.PooledConnection 接口中的 addConnectionEventListener 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成员](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 类](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
