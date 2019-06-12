---
title: prepare 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.prepare
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f800c966-3fae-41b3-963a-464988f80da3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: acf6efd0799b129ed06ab272a67e5bf6bebfb05c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771027"
---
# <a name="prepare-method-sqlserverxaresource"></a>prepare 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  请求资源管理器为提交给定 Xid 对象所指定的事务做好准备。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int prepare(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>Parameters  
 *xid*  
  
 一个 Xid 的对象。  
  
## <a name="return-value"></a>返回值  
 **Int**值。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 prepare 方法是由 javax.transaction.xa.XAResource 接口中的 prepare 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
