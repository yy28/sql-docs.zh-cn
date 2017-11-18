---
title: "supportsExpressionsInOrderBy 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
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
- SQLServerDatabaseMetaData.supportsExpressionsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 858f3c02-4531-4775-97e9-a03b316bdaba
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dc260d583a7ee26647d00863b9027b73efba5a69
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="supportsexpressionsinorderby-method-sqlserverdatabasemetadata"></a>supportsExpressionsInOrderBy 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否支持 ORDER BY 列表中的表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean supportsExpressionsInOrderBy()  
```  
  
## <a name="return-value"></a>返回值  
 **true**如果支持。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 supportsExpressionsInOrderBy 方法指定此 supportsExpressionsInOrderBy 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

