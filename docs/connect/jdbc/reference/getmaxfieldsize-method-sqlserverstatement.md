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
manager: craigg
ms.openlocfilehash: de123b3c6c8f0105a7280c87a4983fadc657ad93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795605"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可为由此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象生成的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的字符和二进制列值返回的最大字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>返回值  
 指示列可包含的最大字节数的 int；如果没有限制，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMaxFieldSize 方法由 java.sql.Statement 接口中的 getMaxFieldSize 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 方法](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
