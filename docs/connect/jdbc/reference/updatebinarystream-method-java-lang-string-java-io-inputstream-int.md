---
description: updateBinaryStream 方法 (java.lang.String, java.io.InputStream, int)
title: updateBinaryStream 方法 (java.io.InputStream, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBinaryStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9be246a7-85fa-49fc-ad79-aabe97f5b280
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47085362965b35f1da9c6c188821709da4c7a3d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472099"
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-int"></a>updateBinaryStream 方法 (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用将具有指定字节数的二进制流值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>参数  
 columnLabel**  
  
 一个包含列标签的字符串。  
  
 *x*  
  
 InputStream 对象。  
  
 *length*  
  
 指示流长度的 int****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateBinaryStream 方法是由 java.sql.ResultSet 接口中的 updateBinaryStream 方法指定的。  
  
 此方法将来自 InputStream 对象的字节传递给所选的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 二进制列，例如 binary、varbinary、varbinary(max)、image、xml 和 udt。 此方法不支持更新字符列。 若要使用 InputStream 更新字符列，请使用 [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) 方法。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常**。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度**。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [updateBinaryStream 方法 (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md)。  
  
## <a name="see-also"></a>另请参阅  
 [updateBinaryStream 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
