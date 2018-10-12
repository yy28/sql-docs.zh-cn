---
title: setCharacterStream 方法 (int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cb6ac7f5-81ae-4cb7-87c8-cbee40d278c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ce5694d1f594c69e6f7f72cc7abb497e65bf250
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732635"
---
# <a name="setcharacterstream-method-int-javaioreader-long"></a>setCharacterStream 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为具有指定字符数长度的 java.io.Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 指示参数编号的 int。  
  
 reader  
  
 包含 Unicode 数据的 java.io.Reader 对象。  
  
 *length*  
  
 指示流中字符数的 long。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setCharacterStream 方法由 java.sql.PreparedStatement 接口中的 setCharacterStream 方法指定。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [setCharacterStream 方法 &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setCharacterStream 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
