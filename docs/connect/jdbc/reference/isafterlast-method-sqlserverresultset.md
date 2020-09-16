---
description: isAfterLast 方法 (SQLServerResultSet)
title: isAfterLast 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f0f982ebfce1e4920c98583f31bb7a9e14ba867
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433669"
---
# <a name="isafterlast-method-sqlserverresultset"></a>isAfterLast 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索游标是否位于此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的最后一行之后。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>返回值  
 如果游标位于最后一行之后，则值为 true****。 如果游标在任何其他位置或结果集不包含任何行，则为 false****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isAfterLast 方法是由 java.sql.ResultSet 接口中的 isAfterLast 方法指定的。  
  
 如果将此方法用于动态游标（包括只进只读游标）且将 selectMethod 连接属性设置为“cursor”，会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
