---
description: updateDouble 方法 (java.lang.String, double)
title: updateDouble 方法 (java.lang.String, double) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDouble (java.lang.String, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f70971d5-34cc-4f70-8a91-5d46356b24ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8a142c0265b013b95faabd6546978dfabdfe6e0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353443"
---
# <a name="updatedouble-method-javalangstring-double"></a>updateDouble 方法 (java.lang.String, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的列名称使用 double**** 值更新指定的列。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateDouble(java.lang.String columnName,  
                         double x)  
```  
  
#### <a name="parameters"></a>参数  
 *columnName*  
  
 一个包含列名的字符串  。  
  
 *x*  
  
 double**** 值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateDouble 方法是由 java.sql.ResultSet 接口中的 updateDouble 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [updateDouble 方法 (SQLServerResultSet)](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
