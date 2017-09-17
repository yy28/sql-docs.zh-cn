---
title: "getShort 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文档"
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
- SQLServerResultSet.getShort (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 183af414-b0a3-4ca7-b160-d199bcf469b0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d79623af5f99395070abc2b4054ed9cd5276a3a1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getshort-method-javalangstring-sqlserverresultset"></a>getShort 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此当前行中的指定的列名称的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象作为**短**Java 编程语言中。  
  
## <a name="syntax"></a>语法  
  
```  
  
public short getShort(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 A**字符串**包含列名称。  
  
## <a name="return-value"></a>返回值  
 A**短**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getShort 方法指定此 getShort 方法。  
  
 仅在支持此方法[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]可以安全地返回如 smallint、 tinyint 和位的整数值的数据类型。 在任何其他数据类型上使用此方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getShort 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
