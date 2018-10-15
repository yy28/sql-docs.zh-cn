---
title: SQLServerXAResource 成员 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9d55da45733e15a9b2aa98f7c6d8fa386b1e4e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682685"
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了由 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 类公开的成员。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
  
|名称|描述|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|用于允许使用紧密结合的 XA 事务，这些事务具有不同的 XA 分支事务 ID (XID)，但具有相同的全局事务 ID (GTRID)。|  
  
## <a name="inherited-fields"></a>继承的字段  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN、TMFAIL、TMJOIN、TMNOFLAGS、TMONEPHASE、TMRESUME、TMSTARTRSCAN、TMSUCCESS、TMSUSPEND、XA_OK、XA_RDONLY|  
  
## <a name="methods"></a>方法  
  
|名称|描述|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|提交由给定的 Xid 对象所指定的全局事务。|  
|[end](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|结束代表某个事务分支执行的工作。|  
|[forget](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|通知资源管理器忘记试探完成的事务分支。|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|获取为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置的当前事务超时值。|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|确定目标对象所表示的资源管理器实例是否与给定 XAResource 对象所表示的资源管理器实例相同。|  
|[prepare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|请求资源管理器为提交给定 Xid 对象所指定的事务做好准备。|  
|[恢复 (recover)](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|从资源管理器获取准备好的事务分支的列表。|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|请求资源管理器回滚代表事务分支执行的工作。|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|为此 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 对象设置当前事务超时值。|  
|start[](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|开始代表在 Xid 对象中指定的事务分支工作。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
