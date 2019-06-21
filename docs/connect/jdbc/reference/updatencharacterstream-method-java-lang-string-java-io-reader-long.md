---
title: updateNCharacterStream 方法 String - Reader - long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: db0a96a8-248f-4664-9c13-f480f309ab91
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7285f091a933ebbcfa4796da338e34c6795105fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798469"
---
# <a name="updatencharacterstream-method-javalangstring-javaioreader-long"></a>updateNCharacterStream 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将具有指定字节数的字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateNCharacterStream(java.lang.String columnLabel,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnLabel   
  
 一个包含列标签的字符串  。  
  
 reader   
  
 Reader 对象。  
  
 *length*  
  
 流的长度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateNCharacterStream 方法由 java.sql.ResultSet 接口中的 updateNCharacterStream 方法指定。  
  
 此方法将来自要选择的读取器对象中传递 Unicode 字符**nchar**， **nvarchar （max)** ， **ntext**，以及**xml**列。 在其他数据类型列上使用此方法会引发异常。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [updateNCharacterStream 方法 &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-java-lang-string-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [updateNCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
