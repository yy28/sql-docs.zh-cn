---
title: findColumn 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24aed500f5b345e2ba3762bdd7a888fc5f8f31ba
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954574"
---
# <a name="findcolumn-method-sqlserverresultset"></a>findColumn 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中给定列名称的首个匹配列的索引。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>parameters  
 *columnName*  
  
 包含列名称的 String  。  
  
## <a name="return-value"></a>返回值  
 指示列索引的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 findColumn 方法是由 java.sql.ResultSet 接口中的 findColumn 方法指定的。  
  
 如果存在多个同名的列，findColumn 方法将返回第一个区分大小写的匹配项。 如果没有区分大小写的匹配项，此方法返回第一个不区分大小写的匹配项。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
