---
title: isBeforeFirst 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ffe17993b3a03563ec20e8f509e6eae2f6ed47cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977788"
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>isBeforeFirst 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索游标是否位于此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的第一行之前。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>返回值  
 如果游标位于第一行之前,**则为 true** 。 如果游标位于任何其他位置, 或者如果结果集不包含任何行, 则**为 false** 。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 isBeforeFirst 方法由 isBeforeFirst 方法在方法中指定。  
  
 如果将此方法用于动态游标（包括只进只读游标）且将 selectMethod 连接属性设置为“cursor”，会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
