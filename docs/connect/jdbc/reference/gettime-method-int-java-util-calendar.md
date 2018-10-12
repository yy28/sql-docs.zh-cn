---
title: setTime 方法 (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 87b7fbaf-7149-494f-b3b2-16b468a8ebf1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5c0172dd04e13775b977a93f05f2976791a2343
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611906"
---
# <a name="gettime-method-int-javautilcalendar"></a>getTime 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引，使用给定的 Calendar 对象检索 Java 编程语言中指定参数作为 java.sql.Time 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Time getTime(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示参数索引的 int。  
  
 *cal*  
  
 一个日历对象。  
  
## <a name="return-value"></a>返回值  
 一个时间对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getTime 方法是由 java.sql.CallableStatement 接口中的 getTime 方法指定的。  
  
 在查看标题为"Getter 方法转换"的图表[了解数据类型转换](../../../connect/jdbc/understanding-data-type-conversions.md)以查看哪个[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可通过此方法检索的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [getTime 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
