---
title: getTimestamp 方法 (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2dd5688-7344-437a-8716-7024fb8e9c31
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 469cc5febe96b84e3df05a6b56fbb5367efce155
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778713"
---
# <a name="gettimestamp-method-int-javautilcalendar-sqlserverresultset"></a>getTimestamp 方法 (int, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  通过使用 Calendar 对象检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象当前行中指定列索引的值作为 Java 编程语言中的 java.sql.Timestamp 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Timestamp getTimestamp(int columnIndex,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 cal   
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTimestamp 方法由 java.sql.ResultSet 接口中的 getTimestamp 方法指定。  
  
 此方法只从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 和 smalldatetime 列返回值。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
