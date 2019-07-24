---
title: setNCharacterStream 方法到读取器对象-长 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af9a1ba8-7980-43fa-88e5-14f6cc5e897c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73bd7fe7d3da0745f66e0a6d883d7024a318c95f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973889"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader-long"></a>setNCharacterStream 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为具有指定字符数长度的指定 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                     java.io.Reader value,  
                     long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName   
  
 指示参数名称的字符串  。  
  
 *value*  
  
 Reader 对象。  
  
 *length*  
  
 指示流中字符数的 long  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNCharacterStream 方法由 setNCharacterStream 方法在 CallableStatement 接口中指定。  
  
 应将此方法用于**NCHAR**、 **NVARCHAR**、 **NTEXT**和**XML**数据类型。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [setNCharacterStream 方法 &#40;java.lang.String, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-java-lang-string-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
