---
title: "getNString 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 744690d35d6f9b3357939a7cd05b885e2579917c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定列的当前行中的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)作为 java.lang.String 对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 包含列标签的字符串。  
  
## <a name="return-value"></a>返回值  
 一个字符串对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.SQLServerResultSet 接口中的 getNString 方法指定此 getNString 方法。  
  
 此方法可以用于检索的值**nvarchar**， **nchar**， **nvarchar (max)**， **ntext**，或**xml**此当前行中的列[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。 如果尝试使用此方法检索其他数据类型的值，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNString 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
