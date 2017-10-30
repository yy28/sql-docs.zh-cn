---
title: "getTime 方法 （java.lang.String，java.util.Calendar） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eaa53198cb3a96725f3304a7bb8fa88c67df73b1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>getTime 方法 (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  作为 Java 编程语言中，由参数名称，使用给定的日历对象中的 java.sql.Time 对象中检索指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 A**字符串**，其中包含参数名称。  
  
 *cal*  
  
 日历对象中。  
  
## <a name="return-value"></a>返回值  
 一个时间对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetTime 方法 java.sql.CallableStatement 界面中指定此 getTime 方法。  
  
 请参阅中的图表标题为"Getter 方法转换"[了解数据类型转换](../../../connect/jdbc/understanding-data-type-conversions.md)查看哪些[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以使用此方法检索数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [getTime 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

