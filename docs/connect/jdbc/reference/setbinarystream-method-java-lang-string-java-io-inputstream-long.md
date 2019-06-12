---
title: setBinaryStream 方法来输入流的长时间 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d59c7327-c9dc-4e4f-9dff-19e1a3c62eb2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 65c4a60dbd9dd4d7f0d3ffd59897262679b9a656
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764718"
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream-long"></a>setBinaryStream 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的输入流，而指定输入流将含有指定字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x,  
                            long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName   
  
 一个字符串，该字符串包含参数的名称  。  
  
 *x*  
  
 InputStream 对象。  
  
 *length*  
  
 以字节数指示长度的 long  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setBinaryStream 方法由 java.sql.CallableStatement 接口中的 setBinaryStream 方法指定。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，我们建议使用 JDBC 4.0 方法 [setBinaryStream 方法 (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setBinaryStream (SQLServerCallableStatement)](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
