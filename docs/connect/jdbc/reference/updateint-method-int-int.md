---
title: updateInt 方法 （int，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateInt (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f4f651b0-a822-4bd4-b391-cc2355154a2a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f5e69e13762bdfb9b6adde9f635588bc35b742c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797185"
---
# <a name="updateint-method-int-int"></a>updateInt 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定列索引，使用 int  值更新指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateInt(int index,  
                      int x)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示列索引的 int  。  
  
 *x*  
  
 **Int**值。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 updateInt 方法是由 java.sql.ResultSet 接口中的 updateInt 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateInt 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
