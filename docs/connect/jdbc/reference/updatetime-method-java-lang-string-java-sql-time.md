---
description: updateTime 方法 (java.lang.String, java.sql.Time)
title: updateTime 方法 (java.lang.String, java.sql.Time) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateTime (java.lang.String, java.sql.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fbbcef68-b903-4cfd-911c-a7e239d17c74
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36af12218b060175bd708e6d5ca6468c18a7e3f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457922"
---
# <a name="updatetime-method-javalangstring-javasqltime"></a>updateTime 方法 (java.lang.String, java.sql.Time)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用时间值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateTime(java.lang.String columnName,  
                       java.sql.Time x)  
```  
  
#### <a name="parameters"></a>参数  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 时间值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateTime 方法是由 java.sql.ResultSet 接口中的 updateTime 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateTime 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
