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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e516f930d5482b84ffff4827b0ae93225fc8c5a3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919647"
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
  
  
