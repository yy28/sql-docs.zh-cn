---
title: updateBlob 方法 (java.lang.String, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 018cd71b-4b58-49a7-990e-d28dbb12da70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d669f4a675953b38bf0a14b4c3358c86f7f87b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637425"
---
# <a name="updateblob-method-javalangstring-javaioinputstream"></a>updateBlob 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定输入流更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBlob(java.lang.String columnLabel,  
                       java.io.InputStream inputStream)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 一个包含列标签的字符串。  
  
 *inputStream*  
  
 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBlob 方法由 java.sql.ResultSet 接口中的 updateBlob 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
