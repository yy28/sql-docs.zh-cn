---
title: "cancel 方法 (SQLServerStatement) |Microsoft 文档"
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
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b906ee23d28e42ff105d5d9bb919453193d90f68
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cancel-method-sqlserverstatement"></a>cancel 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取消当前正在此运行的 SQL 语句[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的取消方法指定此取消方法。  
  
 当执行可生成单个大型只进、只读结果集的语句时，您所感兴趣的可能只是返回的结果集中的一些初始行集。 在这种情况下，应用程序可能调用[取消](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)之前关闭结果相关联的语句对象方法设置以尽量减少放弃所做的剩余的不必要行所需的处理时间。 在决定是否应使用此方法时，建议对照可节约的处理时间与取消执行所需的时间及与服务器之间的附加往返，在两者之间进行折衷。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

