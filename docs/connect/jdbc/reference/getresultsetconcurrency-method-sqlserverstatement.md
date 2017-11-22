---
title: "getResultSetConcurrency 方法 (SQLServerStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.getResultSetConcurrency
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 47ef6547-5ec7-4cf5-a4d4-e34cbeec72eb
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf280b34ed771d4d92e41e4689eb3343a6aa994e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getresultsetconcurrency-method-sqlserverstatement"></a>getResultSetConcurrency 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索结果集的并发性[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)此生成的对象[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getResultSetConcurrency()  
```  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示结果集并发类型。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 getResultSetConcurrency 方法指定此 getResultSetConcurrency 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
