---
title: previous 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.previous
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66eb4e10-c375-4b31-ac46-3ba1d9dbf6a0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e2eb9db321fc8c2b8b20ca41b685cb27f8595072
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798721"
---
# <a name="previous-method-sqlserverresultset"></a>previous 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将游标移到此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的上一行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean previous()  
```  
  
## <a name="return-value"></a>返回值  
 **true**新的当前行是否有效。 **false**如果没有要处理的多个行。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此以前方法由 java.sql.ResultSet 接口中的上一方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
