---
title: getConcurrency 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d0d59186e15dc07d1d4e91ac673c456ec592d01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952827"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的并发模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>返回值  
 指明并发类型的 int  值，可取值如下：  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getConcurrency 方法由 getConcurrency 方法在方法中指定。  
  
 使用的并发类型是由创建结果集的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象决定的。  
  
 此方法可以用于确定实际并发类型。 如果应用程序选择了 CONCUR_READ_ONLY 或 CONCUR_UPDATABLE，将返回这些并发类型。 如果应用程序使用了默认并发类型，将返回 CONCUR_READ_ONLY。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
