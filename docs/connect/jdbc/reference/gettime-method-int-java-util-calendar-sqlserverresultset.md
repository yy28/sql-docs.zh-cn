---
title: getTime 方法 (int, java.util.Calendar) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d21e0c1d-9d6e-468f-8b11-cc7209b2c2e5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03acff226a453ce96ab05043b9241468fb35ea9e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785913"
---
# <a name="gettime-method-int-javautilcalendar-sqlserverresultset"></a>getTime 方法 (int, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  通过使用给定的 Calendar 对象，检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引的值作为 Java 编程语言中的 java.sql.Time 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Time getTime(int columnIndex,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
 *cal*  
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 一个对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTime 方法由 java.sql.ResultSet 接口中的 getTime 方法指定。  
  
 此方法返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 数据类型的有效时间部分，日期部分设置为采用所提供的 Calendar 时区的 Java 基线日期 1970/01/01。  
  
## <a name="see-also"></a>另请参阅  
 [getTime 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
