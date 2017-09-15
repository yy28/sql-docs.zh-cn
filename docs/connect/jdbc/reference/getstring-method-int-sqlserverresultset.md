---
title: "getString 方法 (int) (SQLServerResultSet) |Microsoft 文档"
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
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2851090b2f22faac3f050ad535ec9f36ac3efae6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-int-sqlserverresultset"></a>getString 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中指定的列索引的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**字符串**Java 编程语言中。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *列索引*  
  
 **Int** ，该值指示的列索引。  
  
## <a name="return-value"></a>返回值  
 A**字符串**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 GetString 方法 java.sql.ResultSet 界面中指定此 getString 方法。  
  
 中的所有列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以作为字符串返回。 这意味着，**字符串**表示形式所有基于数字的和基于字符的类型，并且的十六进制字符串表示形式如二进制、 varbinary、 varbinary （max）、 图像、 时间戳和 uniqueidentifier、 二进制列可以是返回。  
  
 如 money、 smallmoney、 datetime、 smalldatetime、 float、 real、 小数和数值的区分位置的类型将返回类型的基础值的规范的 tostring （） 格式。  
  
 用户定义类型以十六进制形式返回**字符串**值。  
  
## <a name="see-also"></a>另请参阅  
 [getString 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
