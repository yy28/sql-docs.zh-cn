---
title: updateShort 方法 (int，short) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (int, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 155b9189-cb97-4264-b42c-bbda1c7d624f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e00abb9a2590f0e3fe34608e89280df7a50fad7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799376"
---
# <a name="updateshort-method-int-short"></a>updateShort 方法 (int, short)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列索引使用 short  值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateShort(int index,  
                        short x)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示列索引的 int  。  
  
 *x*  
  
 一个**短**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateShort 方法是由 java.sql.ResultSet 接口中的 updateShort 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateShort 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
