---
title: updateObject 方法 (int, java.lang.Object, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateObject (int, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9d33571b-4887-49d3-96df-8abda7b5a904
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6bcee9c77c6b015255ab1d3127047cecd802bbda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698535"
---
# <a name="updateobject-method-int-javalangobject-int"></a>updateObject 方法 (int, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列索引和小数位数使用 Object 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateObject(int index,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引  
  
 指示列索引的 int。  
  
 obj  
  
 Object 值。  
  
 *scale*  
  
 对于 java.sql.Types.DECIMAL 或 java.sql.Types.NUMERIC 类型，这是小数点后的位数。 对于所有其他类型，则忽略此值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另请参阅  
 [updateObject 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
