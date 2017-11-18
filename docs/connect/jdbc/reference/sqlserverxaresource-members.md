---
title: "SQLServerXAResource 成员 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57004473ae83a98797992585baed5959e0874dcc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource 成员
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出了通过公开的成员[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)类。  
  
## <a name="constructors"></a>构造函数  
 无。  
  
## <a name="fields"></a>字段  
  
|Name|Description|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|用于允许使用紧密结合的 XA 事务，这些事务具有不同的 XA 分支事务 ID (XID)，但具有相同的全局事务 ID (GTRID)。|  
  
## <a name="inherited-fields"></a>继承的字段  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN、TMFAIL、TMJOIN、TMNOFLAGS、TMONEPHASE、TMRESUME、TMSTARTRSCAN、TMSUCCESS、TMSUSPEND、XA_OK、XA_RDONLY|  
  
## <a name="methods"></a>方法  
  
|Name|Description|  
|----------|-----------------|  
|[提交](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|提交全局给定 Xid 对象所指定的事务。|  
|[结束](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|结束代表某个事务分支执行的工作。|  
|[忘记](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|通知资源管理器忘记试探完成的事务分支。|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|获取为此参数设置的当前事务超时值[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)对象。|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|确定目标对象所表示的资源管理器实例是否与给定的 XAResource 对象所表示的资源管理器实例相同。|  
|[准备](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|资源管理器准备由给定 Xid 对象指定的事务的事务提交的请求。|  
|[恢复 (recover)](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|从资源管理器获取准备好的事务分支的列表。|  
|[回滚](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|请求资源管理器回滚代表事务分支执行的工作。|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|此设置当前的事务超时值[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)对象。|  
|[启动](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|启动工作代表 Xid 对象中指定的事务分支。|  
  
## <a name="inherited-methods"></a>继承的方法  
  
|类继承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone、 equals、 finalize、 getClass、 hashCode、 notify、 notifyAll、 toString、 wait|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerXAResource 类](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

