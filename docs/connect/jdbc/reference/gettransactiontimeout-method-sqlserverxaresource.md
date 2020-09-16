---
description: getTransactionTimeout 方法 (SQLServerXAResource)
title: getTransactionTimeout 方法 (SQLServerXAResource) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8b8605ab9c9acf4872a93ed305da7cb01fef85c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433999"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>getTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  获取为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置的当前事务超时值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>例外  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>注解  
 此 getTransactionTimeout 方法是由 javax.transaction.xa.XAResource 接口中的 getTransactionTimeout 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
