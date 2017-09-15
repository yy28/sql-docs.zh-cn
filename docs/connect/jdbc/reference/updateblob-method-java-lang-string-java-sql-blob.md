---
title: "updateBlob 方法 （java.lang.String，java.sql.Blob） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.updateBlob (java.lang.String, java.sql.Blob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fdd47885-c7ec-4599-a645-ad0e082586f4
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca6d6ef314233bec50c74f60e0341728400e60c6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updateblob-method-javalangstring-javasqlblob"></a>updateBlob 方法 (java.lang.String, java.sql.Blob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.Blob 值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBlob(java.lang.String columnName,  
                       java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 A**字符串**包含列名称。  
  
 *x*  
  
 一个 Blob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 updateBlob 方法指定此 updateBlob 方法。  
  
## <a name="see-also"></a>另请参阅  
 [updateBlob 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
