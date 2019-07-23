---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233599694c4fb4f7764bbb48d5c77e0fcd273340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977847"
---
# <a name="isafterlast-method-sqlserverresultset"></a>isAfterLast 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索游标是否位于此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的最后一行之后。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>返回值  
 如果光标位于最后一行之后,**则为 true** 。 如果游标位于任何其他位置, 或者如果结果集不包含任何行, 则**为 false** 。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 isAfterLast 方法由 isAfterLast 方法在方法中指定。  
  
 如果将此方法用于动态游标（包括只进只读游标）且将 selectMethod 连接属性设置为“cursor”，会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
