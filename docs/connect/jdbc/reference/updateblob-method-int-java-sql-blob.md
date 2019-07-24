---
title: updateBlob 方法 (int, .sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBlob (int, java.sql.Blob)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e86f588-1365-4011-9412-f0acf7009880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ce5c1c2e8ce635e5b53f5b5e609666e39e36bc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997139"
---
# <a name="updateblob-method-int-javasqlblob"></a>updateBlob 方法 (int, java.sql.Blob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.Blob 值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateBlob(int index,  
                       java.sql.Blob x)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示列索引的 int  。  
  
 *x*  
  
 Blob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateBlob 方法是由 java.sql.ResultSet 接口中的 updateBlob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateBlob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
