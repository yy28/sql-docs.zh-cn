---
title: setTransactionTimeout 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81bf280397b2ba1ddac428eb12c882af2b31e1b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615505"
---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置当前事务超时值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parameters  
 *seconds*  
  
 **Int**值。  
  
## <a name="return-value"></a>返回值  
 如果已成功设置超时值，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 setTransactionTimeout 方法由 javax.transaction.xa.XAResource 接口中的 setTransactionTimeout 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
