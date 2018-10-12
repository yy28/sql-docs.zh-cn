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
manager: craigg
ms.openlocfilehash: 8ec96cd3f56b1710268ae951e39e98866fe1bd54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826815"
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
  
 **Int**可以采用以下值之一的值： XAResource.TMSTARTRSCAN 或 XAResource.TMENDRSCAN 或 XAResource.TMNOFLAGS 或 XAResource.TMSTARTTRSCAN |XAResource.TMENDRSCAN。  
  
## <a name="return-value"></a>返回值  
 一个 Xid 的对象。  
  
## <a name="exceptions"></a>异常  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 此 recover 方法是由 javax.transaction.xa.XAResource 接口中的 recover 方法指定的。  
  
 如果将参数**标志**不 XAResource.TMSTARTRSCAN |XAResource.TMENDRSCAN，则恢复扫描一定正在进行。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成员](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
