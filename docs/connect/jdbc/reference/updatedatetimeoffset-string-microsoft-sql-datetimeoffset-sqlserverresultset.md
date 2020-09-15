---
description: updateDateTimeOffset(string, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
title: updateDateTimeOffset(string) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 952947ce-7c6e-4364-b035-46cb7fe621b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d482c1b4fb9f70e2197601f01eca176da4b3f0c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353723"
---
# <a name="updatedatetimeoffsetstring-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(string, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此方法。  
  
 根据给定的列名称，将指定的列值更新为 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>参数  
 *columnName*  
  
 列的名称。  
  
 *x*  
  
 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 可以使用 [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md) 检索 [DateTimeOffset 类](../../../connect/jdbc/reference/datetimeoffset-class.md)值。  
  
## <a name="see-also"></a>另请参阅  
 [updateDateTimeOffset (SQLServerResultSet)](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
