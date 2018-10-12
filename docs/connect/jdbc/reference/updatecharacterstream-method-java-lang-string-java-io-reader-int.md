---
title: updateCharacterStream 方法 (java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateCharacterStream (java.lang.String, java.io.Reader, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 08cfc4e0-83f0-4f2f-ac55-b381f34fe67f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84eb71761702fe48fd8001f7789fea5a5e47f586
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810795"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader-int"></a>updateCharacterStream 方法 (java.lang.String, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将有指定字符数的字符流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateCharacterStream(java.lang.String columnName,  
                                  java.io.Reader readerValue,  
                                  int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
 *readerValue*  
  
 一个读取器对象。  
  
 *length*  
  
 指示流长度的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateCharacterStream 方法由 java.sql.ResultSet 接口中的 updateCharacterStream 方法指定。  
  
 此方法将来自 Reader 对象的 Unicode 字符传递给所选文本和二进制列。 这包括所有文本列与 binary、varbinary、varbinary(max)、image 和 xml 列，但不包括 udt 列。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [updateCharacterStream 方法 (java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/updatecharacterstream-method-java-lang-string-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [updateCharacterStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
