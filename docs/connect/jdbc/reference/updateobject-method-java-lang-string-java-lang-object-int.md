---
title: updateObject 方法 (java.lang.String, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 27283ce1-637e-4e2c-91ee-8ad379114ac5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10959976eb6c3c9908d7f5953a8a2edb1c1328c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654906"
---
# <a name="updateobject-method-javalangstring-javalangobject-int"></a>updateObject 方法 (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称和小数位数使用 Object 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnName*  
  
 一个包含列名的字符串。  
  
 obj  
  
 Object 值。  
  
 *scale*  
  
 对于 java.sql.Types.DECIMAL 或 java.sql.Types.NUMERIC 类型，这是小数点后的位数。 对于所有其他类型，则忽略此值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateObject 方法由 java.sql.ResultSet 接口中的 updateObject 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [updateObject 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
