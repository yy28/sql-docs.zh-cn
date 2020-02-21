---
title: updateShort 方法 (java.lang.String, short) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (java.lang.String, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e596e99-11ce-4a57-b247-e40078922036
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d084c129552b0979f773adc582d0b25ea6e3f39
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68213644"
---
# <a name="updateshort-method-javalangstring-short"></a>updateShort 方法 (java.lang.String, short)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用短值更新指定的列  。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateShort(java.lang.String columnName,  
                        short x)  
```  
  
#### <a name="parameters"></a>parameters  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 short  值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateShort 方法是由 java.sql.ResultSet 接口中的 updateShort 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateShort 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
