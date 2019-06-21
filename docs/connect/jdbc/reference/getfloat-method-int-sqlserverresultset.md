---
title: getFloat 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30863ef5-7a7c-440e-8fbb-426a99266ee1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 72a2ed57b9b86db50c7d0c1f824181c4a5623026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802012"
---
# <a name="getfloat-method-int-sqlserverresultset"></a>getFloat 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Java 编程语言中的 float  的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public float getFloat(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 一个**float**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getFloat 方法是由 java.sql.ResultSet 接口中的 getFloat 方法指定的。  
  
 此方法使用 Java float  精度返回基于数字的所有类型。  
  
## <a name="see-also"></a>另请参阅  
 [getFloat 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
