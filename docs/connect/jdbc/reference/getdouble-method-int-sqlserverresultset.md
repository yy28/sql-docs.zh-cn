---
title: getDouble 方法 (int) (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 128df26a-9063-4bdf-a4fb-a077cbe7cfe1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77589b13639f678b0c647241054075ec26151e5b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635215"
---
# <a name="getdouble-method-int-sqlserverresultset"></a>getDouble 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Java 编程语言中的 double 的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public double getDouble(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 一个**double**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getDouble 方法由 java.sql.ResultSet 接口中的 getDouble 方法指定。  
  
 此方法使用 Java double 精度返回所有基于数字的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [getDouble 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
