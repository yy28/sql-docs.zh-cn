---
title: "updateBinaryStream 方法 （java.io.InputStream，int） |Microsoft 文档"
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
- SQLServerResultSet.updateBinaryStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9be246a7-85fa-49fc-ad79-aabe97f5b280
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1199bdd667e4b24c39f987a37f48f841176ae05
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-int"></a>updateBinaryStream 方法 (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将具有指定字节数的二进制流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 AStringthat 包含列标签。  
  
 *x*  
  
 一个 InputStream 对象中。  
  
 *length*  
  
 **Int** ，该值指示流的长度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateBinaryStream 方法指定此 updateBinaryStream 方法。  
  
 此方法将从 InputStream 对象选择传递字节[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]如二进制、 varbinary、 varbinary （max）、 图像、 xml 和 udt 的二进制列。 此方法不支持更新字符列。 若要更新使用 InputStream 字符列，请使用[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)方法。  
  
 如果不同于在指定流的长度时*长度*参数，在更新或插入行时的 JDBC 驱动程序引发异常。  
  
 如果流的长度为未知，*长度*参数可能设置为-1，以指示该驱动程序应接受而不考虑其长度流。 与 sqljdbc4.jar，我们建议你使用 JDBC 4.0 方法[updateBinaryStream 方法 &#40;java.lang.String、 java.io.InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md)当应用程序希望更新的列从一个流，其长度为未知。  
  
## <a name="see-also"></a>另请参阅  
 [updateBinaryStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
