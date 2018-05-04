---
title: getTimestamp 方法 （java.lang.String，java.util.Calendar） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44474000-8951-49ee-93a5-c8cb879eaf55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00d77a3dcd8ae8a6666ee5419cd0b49be921d93f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
 *ColName*  
  
 一个包含列名的字符串。  
  
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
 [getTimestamp 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
