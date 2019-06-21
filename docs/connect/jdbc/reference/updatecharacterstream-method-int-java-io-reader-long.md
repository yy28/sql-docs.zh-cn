---
title: updateCharacterStream 方法 (java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c426b0e3-2f9d-425a-b7da-1d0325e292d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7a3747df1ff5f64b0f7ebdfa1ff383eb497a8d0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66784220"
---
# <a name="updatecharacterstream-method-int-javaioreader-long"></a>updateCharacterStream 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将有指定字符数的字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x,  
                                  long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnIndex   
  
 指示列索引的 int  。  
  
 *x*  
  
 Reader 对象。  
  
 *length*  
  
 流的长度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateCharacterStream 方法由 java.sql.ResultSet 接口中的 updateCharacterStream 方法指定。  
  
 此方法将来自 Reader 对象的 Unicode 字符传递给所选文本和二进制列。 这包括所有文本列与 binary、varbinary、varbinary(max)、image 和 XML 列，但不包括 UDT 列。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [updateCharacterStream 方法 (int, java.io.Reader)](../../../connect/jdbc/reference/updatecharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [updateCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
