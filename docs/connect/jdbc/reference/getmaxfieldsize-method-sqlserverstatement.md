---
title: getMaxFieldSize 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a1700cc8bb2bfb54dd9ddee52da54899f764650
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982103"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可为由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的字符和二进制列值返回的最大字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>返回值  
 指示列可包含的最大字节数的 int  ；如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxFieldSize 方法由 getMaxFieldSize 方法在 .sql 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 方法](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
