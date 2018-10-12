---
title: updateBlob 方法 (java.lang.String, java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 40f75549-5d5a-4de3-a271-4b8f0dd7b124
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eeedbd023fc6863f6bba75dfe9e1f41c83fd78c1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597182"
---
# <a name="updateblob-method-javalangstring-javaioinputstream-long"></a>updateBlob 方法 (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的将有指定字节数的输入流更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
                                              long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 一个包含列标签的字符串。  
  
 *inputStream*  
  
 InputStream 对象。  
  
 *length*  
  
 指示流长度的 long。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBlob 方法由 java.sql.ResultSet 接口中的 updateBlob 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
