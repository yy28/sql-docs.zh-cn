---
title: getTransactionTimeout 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.getTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed0a37e9-1132-4d3f-b88f-8be674e852b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e71469a271050e3a5c9e053ed6446d8d603f5a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701355"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>getTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置的当前事务超时值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 getTransactionTimeout 方法由 javax.transaction.xa.XAResource 接口中的 getTransactionTimeout 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
