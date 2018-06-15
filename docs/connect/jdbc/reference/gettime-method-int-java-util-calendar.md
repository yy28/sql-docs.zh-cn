---
title: getTime 方法 （int、 java.util.Calendar） |Microsoft 文档
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
- SQLServerCallableStatement.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 87b7fbaf-7149-494f-b3b2-16b468a8ebf1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e01aa8c9bb2f0f7e4f7ea38e9bcdda4dd128b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838092"
---
# <a name="gettime-method-int-javautilcalendar"></a>getTime 方法 (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  作为 Java 编程语言中，给定的参数索引，使用给定的日历对象中的 java.sql.Time 对象中检索指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Time getTime(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 指示参数索引的 int。  
  
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
 [getTime 方法&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
