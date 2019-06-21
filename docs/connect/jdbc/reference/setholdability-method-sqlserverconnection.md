---
title: setHoldability 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 552eebd0-4c38-43f0-961f-35244f99109b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60d46f8f8792eacd7f1f67a67b2fc9fc56bf5a8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66764470"
---
# <a name="setholdability-method-sqlserverconnection"></a>setHoldability 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将使用此 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 对象创建的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的可保持性更改为给定可保持性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setHoldability(int nNewHold)  
```  
  
#### <a name="parameters"></a>Parameters  
 nNewHold   
  
 包含下列可保持性级别之一的 int  值：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setHoldability 方法由 java.sql.Connection 接口中的 setHoldability 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
