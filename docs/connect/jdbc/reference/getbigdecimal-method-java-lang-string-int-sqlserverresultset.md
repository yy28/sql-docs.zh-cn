---
title: getBigDecimal 方法 (java.lang.String, int) (SQLServerResultSet) | Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 572a1799-c232-400f-b8d8-37a5719a8d5e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 701afddaeaad79356a6b76a05a02f5cff1df1f39
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67953905"
---
# <a name="getbigdecimal-method-javalangstring-int-sqlserverresultset"></a>getBigDecimal 方法 (java.lang.String, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的小数位数检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称的值。  
  
> [!NOTE]  
>  JDBC 规范已不推荐使用此方法， 应改用 [getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string-sqlserverresultset.md) 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String columnName,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *scale*  
  
 指示小数点右边的位数的 int  。  
  
## <a name="return-value"></a>返回值  
 BigDecimal 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getBigDecimal 方法是由 java.sql.ResultSet 接口中的 getBigDecimal 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBigDecimal 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
