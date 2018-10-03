---
title: 上一个方法 (SQLServerResultSet) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 587398c10e693081a9dc6a6c4abb61ff970b2f03
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692315"
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
  
  
