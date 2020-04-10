---
title: getXAResource 方法 (SQLServerXAConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: beee81cbc62a1257c9f9f0fbe8c93720fa54a523
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910133"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 方法 (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象，事务管理器将使用它来管理此 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 对象如何参与分布式事务。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>返回值  
 XAResource 对象。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>备注  
 此 getXAResource 方法是由 javax.sql.XAConnection 接口中的 getXAResource 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAConnection 方法](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 成员](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 类](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
