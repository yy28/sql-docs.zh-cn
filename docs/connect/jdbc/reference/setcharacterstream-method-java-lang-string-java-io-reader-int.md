---
title: setCharacterStream 方法 (java.lang.String, java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 88a8e89e-8817-4161-85b1-9a9a2fd01cdb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27e19162aca466235c9242d2ea4a2f65d7b33630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974697"
---
# <a name="setcharacterstream-method-javalangstring-javaioreader-int"></a>setCharacterStream 方法 (java.lang.String, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为具有指定字符数的指定的 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCharacterStream(java.lang.String parameterName,  
                              java.io.Reader value,  
                              int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName   
  
 一个字符串，该字符串包含参数的名称  。  
  
 *value*  
  
 包含 Unicode 数据的 Reader 对象。  
  
 *length*  
  
 以字符数指示长度的 int  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setCharacterStream 方法由 setCharacterStream 方法在 CallableStatement 接口中指定。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，我们建议使用 JDBC 4.0 方法 [setCharacterStream 方法 (java.lang.String, java.io.Reader)](../../../connect/jdbc/reference/setcharacterstream-method-java-lang-string-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
