---
title: updateClob 方法 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 338a2bf2-b110-469d-ad08-a0f2bbefcb88
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 541ec983b9564d9008724701564b7154102231cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801703"
---
# <a name="updateclob-method-javalangstring-javaioreader"></a>updateClob 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的 Reader 对象更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateClob(java.lang.String columnLabel,  
                        java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parameters  
 columnLabel   
  
 一个包含列标签的字符串  。  
  
 reader   
  
 Reader 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateClob 方法是由 java.sql.ResultSet 接口中的 updateClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
