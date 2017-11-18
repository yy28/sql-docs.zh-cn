---
title: "getTimestamp 方法 （java.lang.String，java.util.Calendar） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getTimestamp (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44474000-8951-49ee-93a5-c8cb879eaf55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa0049c9e48182fc286ae8c247a173955e0b819b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="gettimestamp-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getTimestamp 方法 （java.lang.String，java.util.Calendar） (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言，使用日历对象中的 java.sql.Timestamp 对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String colName,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *colName*  
  
 A**字符串**包含列名称。  
  
 *cal*  
  
 日历对象中。  
  
## <a name="return-value"></a>返回值  
 一个时间戳的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getTimestamp 方法指定此 getTimestamp 方法。  
  
 此方法返回值只能从[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]datetime 和 smalldatetime 列。  
  
## <a name="see-also"></a>另请参阅  
 [getTimestamp 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

