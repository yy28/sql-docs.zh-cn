---
title: recover 方法 (SQLServerXAResource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92d7b0db997a6b77b43efb6d8104f629bb5507e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976021"
---
# <a name="recover-method-sqlserverxaresource"></a>recover 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  从资源管理器获取准备好的事务分支的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>Parameters  
 *flag*  
  
 一个**int**值, 它可以采用以下值之一: XARESOURCE、TMSTARTRSCAN 或 XAResource 或 XAResource 或 TMNOFLAGS |XAResource. TMENDRSCAN。  
  
## <a name="return-value"></a>返回值  
 一个 Xid 对象。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 recover 方法是由 javax.transaction.xa.XAResource 接口中的 recover 方法指定的。  
  
 如果参数**标志**不是 XAResource, 则为 TMSTARTRSCAN 或 XARESOURCE。 TMSTARTRSCAN |XAResource. TMENDRSCAN, 必须进行恢复扫描。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
