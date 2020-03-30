---
title: updateInt 方法 (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateInt (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b0aef8f7-057e-4b57-892c-d120f2daed77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11ee34cd5281fb7db564e965556ff5ee455fb7d0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67998847"
---
# <a name="updateint-method-javalangstring-int"></a>updateInt 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用 int 值更新指定的列  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateInt(java.lang.String columnName,  
                      int x)  
```  
  
#### <a name="parameters"></a>parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 int  值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateInt 方法是由 java.sql.ResultSet 接口中的 updateInt 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateInt 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
