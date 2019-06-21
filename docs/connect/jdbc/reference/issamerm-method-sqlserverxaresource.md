---
title: isSameRM 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6cdfd42d0670d8d536e0a9bf40f2a6981ef5b937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796360"
---
# <a name="issamerm-method-sqlserverxaresource"></a>isSameRM 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  确定目标对象所表示的资源管理器实例是否与给定的 XAResource 对象所表示的资源管理器实例相同。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>Parameters  
 xares   
  
 一个 XAResource 的对象。  
  
## <a name="return-value"></a>返回值  
 如果两个实例相同，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 commit 方法由 javax.transaction.xa.XAResource 接口中的 commit 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
