---
title: "updateAsciiStream 方法 (java.io.InputStream，长) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d426e8b9-62b7-49f8-9863-8697fd3a7085
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d8f10f0f2cda308348db6c654bb35a62c1db333
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updateasciistream-method-javalangstring-javaioinputstream-long"></a>updateAsciiStream 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将有指定字节数的 ASCII 流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateAsciiStream(java.lang.String columnName,  
                              java.io.InputStream streamValue,  
                              long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 A**字符串**包含列名称。  
  
 *streamValue*  
  
 一个 InputStream 对象中。  
  
 *length*  
  
 流的长度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateAsciiStream 方法指定此 updateAsciiStream 方法。  
  
 此方法将从 InputStream 对象 ASCII 字符 （字节） 传递到转换的字符列，其中的 ASCII 范围 [0x00 – 0x7F] Unicode，和 874、 932、 936、 949、 950，和通过 1258年代码页 1250年。 此方法执行到目标排序规则页的转换。 尝试更新不可转换的目标列将引发异常。 对于二进制列，会传递原始字节。  
  
 流的长度是否不同于中指定了什么*长度*参数，在更新或插入行时的 JDBC 驱动程序引发异常。  
  
 如果流的长度为未知，*长度*参数可能设置为-1，以指示该驱动程序应接受而不考虑其长度流。 与 sqljdbc4.jar，我们建议你使用 JDBC 4.0 方法[updateAsciiStream 方法 &#40;java.lang.String、 java.io.InputStream &#41;](../../../connect/jdbc/reference/updateasciistream-method-java-lang-string-java-io-inputstream.md)当应用程序希望更新的列从一个流，其长度为未知。  
  
## <a name="see-also"></a>另请参阅  
 [updateAsciiStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
