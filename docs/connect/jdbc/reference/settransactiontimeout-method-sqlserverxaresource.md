---
title: setTransactionTimeout 方法 (SQLServerXAResource) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d234c7a30553b44fa9ad13c992e3e49116b01505
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926449"
---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置当前事务超时值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>parameters  
 *seconds*  
  
 int  值。  
  
## <a name="return-value"></a>返回值  
 如果已成功设置超时值，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>备注  
 此 setTransactionTimeout 方法是由 javax.transaction.xa.XAResource 接口中的 setTransactionTimeout 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
