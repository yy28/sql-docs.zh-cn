---
title: setCharacterStream 方法 (int, java.io.Reader, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 139a5b74-8d7d-41cf-991a-a142349c58f6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3002c3375f14eb4c33554c960c567e4a3d8526b0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974773"
---
# <a name="setcharacterstream-method-int-javaioreader-int"></a>setCharacterStream 方法 (int, java.io.Reader, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的具有给定字符数的 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setCharacterStream(int n,  
                                     java.io.Reader reader,  
                                     int length)  
```  
  
#### <a name="parameters"></a>parameters  
 *n*  
  
 指示参数编号的 int  。  
  
 reader   
  
 Reader 对象。  
  
 *length*  
  
 字符数。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setCharacterStream 方法是由 java.sql.PreparedStatement 接口中的 setCharacterStream 方法指定的。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常  。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度  。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [setCharacterStream 方法 &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
