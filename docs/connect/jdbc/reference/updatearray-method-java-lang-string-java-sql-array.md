---
description: updateArray 方法 (java.lang.String, java.sql.Array)
title: updateArray 方法 (java.lang.String, java.sql.Array) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateArray (java.lang.String, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6f2ced5a-1c7d-439a-aaa5-472b9f4fdeab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b40ee796c388c19796761eae067132862fddeb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458037"
---
# <a name="updatearray-method-javalangstring-javasqlarray"></a>updateArray 方法 (java.lang.String, java.sql.Array)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用 Array 对象更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateArray(java.lang.String columnName,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>参数  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 Array 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateArray 方法是由 java.sql.ResultSet 接口中的 updateArray 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateArray 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
