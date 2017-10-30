---
title: "insertRow 方法 (SQLServerResultSet) |Microsoft 文档"
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
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9297b57b1ad4ded2611fadb1034a61046e3a4d25
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="insertrow-method-sqlserverresultset"></a>insertRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将插入行的内容添加到此[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象和数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 insertRow 方法指定此 insertRow 方法。  
  
 调用此方法时，游标必须位于插入行上。 调用此方法后，游标将保持在插入行并且结果集保持在插入模式下。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

