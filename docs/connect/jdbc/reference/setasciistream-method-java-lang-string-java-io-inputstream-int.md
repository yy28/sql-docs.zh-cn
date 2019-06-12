---
title: setAsciiStream 方法的输入流字节-int |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ea23386-201f-41af-8232-225de3476765
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2da554800f8700cf6b35e43db215f2bfa32149c0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765175"
---
# <a name="setasciistream-method--javalangstring-javaioinputstream-int"></a>setAsciiStream 方法 (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的输入流，而指定输入流将含有指定字节数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setAsciiStream(java.lang.String parameterName,  
                           java.io.InputStream value,  
                           int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName   
  
 包含参数名称的字符串  。  
  
 *value*  
  
 InputStream 对象。  
  
 *length*  
  
 一个整数，指示以字节数表示的长度  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setAsciiStream 方法由 java.sql.CallableStatement 接口中的 setAsciiStream 方法指定。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [setAsciiStream 方法 (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setasciistream-method-java-lang-string-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
