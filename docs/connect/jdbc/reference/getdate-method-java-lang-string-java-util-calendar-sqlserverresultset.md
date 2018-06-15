---
title: getDate 方法 (java.util.Calendar) 列 |Microsoft 文档
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
- SQLServerResultSet.getDate (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fa2a72a-7499-44ec-8f76-a8e646e0190c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5402a16946770f9167c8d3aef17cedf916f11c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834812"
---
# <a name="getdate-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getDate 方法 （java.lang.String，java.util.Calendar） (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 Java 编程语言，使用给定的日历对象中的 java.sql.Date 对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Date getDate(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ColName*  
  
 一个包含列名的字符串。  
  
 *cal*  
  
 日历对象中。  
  
## <a name="return-value"></a>返回值  
 Date 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetDate 方法 java.sql.ResultSet 界面中指定此 getDate 方法。  
  
 此方法返回的有效日期部分的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]datetime 或 smalldatetime 数据类型，其设置为 00:00 （午夜） 提供的日历的时区中的 Java 时间基线的时间部分。  
  
## <a name="see-also"></a>另请参阅  
 [getDate 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
