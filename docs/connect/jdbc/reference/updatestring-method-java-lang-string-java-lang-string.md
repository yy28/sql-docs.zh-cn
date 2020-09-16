---
description: updateString 方法 (java.lang.String, java.lang.String)
title: updateString 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateString (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3a9236bb-a307-45a8-b7d2-c4cbd9b3cb35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fc3d138284b88b1b1fd52554d739848255d7b50
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457969"
---
# <a name="updatestring-method-javalangstring-javalangstring"></a>updateString 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用字符串值更新指定的列****。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateString(java.lang.String columnName,  
                         java.lang.String x)  
```  
  
#### <a name="parameters"></a>参数  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 String**** 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateString 方法是由 java.sql.ResultSet 接口中的 updateString 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateString 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
