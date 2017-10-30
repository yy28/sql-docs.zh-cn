---
title: "getMaxColumnsInOrderBy 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d6af9bb4-c55d-41f4-a266-d10ebee61194
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3db6ca186c991f82c47f85dc0d9a65949a863c9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getmaxcolumnsinorderby-method-sqlserverdatabasemetadata"></a>getMaxColumnsInOrderBy 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库允许在 ORDER BY 子句中的列的最大数目。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getMaxColumnsInOrderBy()  
```  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示最大允许的列数。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getMaxColumnsInOrderBy 方法指定此 getMaxColumnsInOrderBy 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

