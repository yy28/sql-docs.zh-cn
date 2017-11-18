---
title: "isPoolable 方法 (SQLServerStatement) |Microsoft 文档"
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
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29c948e99dcb9411a427e96c1a9a0492c2d8992f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回指示是否可以将语句添加到用户提供的语句池的一个值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果语句可以添加到用户提供语句池;**false**否则为。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)更改能合并行为的对象。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

