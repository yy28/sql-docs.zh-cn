---
title: updateAsciiStream 方法 （java.io.InputStream，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateAsciiStream (int, java.io.InputStream.int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d07944b8-7001-49b5-b3b3-0676f71e17cf
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 808c9095d61cd76c53f2f350fd90a0858162e640
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052664"
---
# <a name="updateasciistream-method-int-javaioinputstream-int"></a>updateAsciiStream 方法 (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将有指定字节数的 ASCII 流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateAsciiStream(int index,  
                              java.io.InputStream x,  
                              int length)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示列索引的 int。  
  
 *x*  
  
 InputStream 对象。  
  
 *length*  
  
 指示流长度的 int。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateAsciiStream 方法由 java.sql.ResultSet 接口中的 updateAsciiStream 方法指定。  
  
 此方法将来自 InputStream 对象的 ASCII 字符（字节）传递给可转换的字符列，即 Unicode 的 ASCII 范围 [0x00 – 0x7F] 以及 874、932、936、949、950 和 1250 到 1258 代码页。 此方法执行到目标排序规则页的转换。 尝试更新不可转换的目标列将引发异常。 对于二进制列，会传递原始字节。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [updateAsciiStream 方法 (int, java.io.InputStream)](../../../connect/jdbc/reference/updateasciistream-method-int-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另请参阅  
 [updateAsciiStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
