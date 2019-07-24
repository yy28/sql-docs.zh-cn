---
title: getBigDecimal 方法 (int, int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c99d0772-b26c-492c-a643-2813b5429993
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15991cb98860ccc471229ae3abb8e3b24e35c799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954014"
---
# <a name="getbigdecimal-method-int-int-sqlserverresultset"></a>getBigDecimal 方法 (int, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定的小数位数检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象当前行中指定列索引的值。  
  
> [!NOTE]  
>  JDBC 规范已不推荐使用此方法， 应改用 [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int-sqlserverresultset.md) 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.math.BigDecimal getBigDecimal(int columnIndex,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 *scale*  
  
 指示小数点右边的位数的 int  。  
  
## <a name="return-value"></a>返回值  
 一个 Java.math.bigdecimal 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getBigDecimal 方法由 getBigDecimal 方法在方法中指定。  
  
## <a name="see-also"></a>另请参阅  
 [getBigDecimal 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
