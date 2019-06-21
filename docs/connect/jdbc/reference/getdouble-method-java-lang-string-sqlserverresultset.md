---
title: getDouble 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3ee26412-43d2-404b-bc05-ffd0fc75805c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fb74dd4b80256ad85e03a258a0adc5d93ba1880d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66765884"
---
# <a name="getdouble-method-javalangstring-sqlserverresultset"></a>getDouble 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 Java 编程语言中的 double  的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public double getDouble(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
## <a name="return-value"></a>返回值  
 一个**double**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getDouble 方法是由 java.sql.ResultSet 接口中的 getDouble 方法指定的。  
  
 此方法使用 Java double 精度返回所有基于数字的数据类型  。  
  
## <a name="see-also"></a>另请参阅  
 [getDouble 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
