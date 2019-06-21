---
title: getNString 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9681ddf0946627306a64c099d2df1c242d95bcbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762807"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列作为 java.lang.String 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnLabel   
  
 一个包含列标签的 String。  
  
## <a name="return-value"></a>返回值  
 一个字符串对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getNString 方法是由 java.sql.SQLServerResultSet 接口中的 getNString 方法指定的。  
  
 此方法可以用于检索的值**nvarchar**， **nchar**， **nvarchar （max)** ， **ntext**，或**xml**的当前行中的列[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 如果尝试使用此方法检索其他数据类型的值，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNString 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
