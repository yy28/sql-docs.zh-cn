---
title: setFetchSize 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 233bf4f8-4758-42d0-a80b-33e34fa78027
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b253ad989593fa88b2281d933387dfe38fee1732
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974253"
---
# <a name="setfetchsize-method-sqlserverresultset"></a>setFetchSize 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为 JDBC 驱动程序提供提示，以指明在此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象需要更多行时应从数据库中提取的行数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parameters  
 *rows*  
  
 指示要提取的行数的 int  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setFetchSize 方法由 setFetchSize 方法在方法中指定。  
  
 如果指定的提取大小为零，JDBC 驱动程序将忽略该值并计算应使用的提取大小。 默认值由创建结果集的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象设置。 可以随时更改提取大小。  
  
 此方法可更改服务器游标的块提取大小，并在下次 JDBC 驱动程序需要调用 sp_cursorfetch 时生效。 如果将提取大小设置为零，将恢复当前使用的游标类型的默认提取大小。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
