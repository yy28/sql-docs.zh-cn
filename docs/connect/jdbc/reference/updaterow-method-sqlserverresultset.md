---
description: updateRow 方法 (SQLServerResultSet)
title: updateRow 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- MSQLServerResultSet.updateRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cfced0ca-a281-40dc-8d2f-370d5f0bf12b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13238fc12a57244116744221fa53b76efde415e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450074"
---
# <a name="updaterow-method-sqlserverresultset"></a>updateRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象当前行的新内容更新基础数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void updateRow()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 updateRow 方法是由 java.sql.ResultSet 接口中的 updateRow 方法指定的。  
  
 游标位于插入行时，无法调用此方法。  
  
 如果在列值未发生任何更改时调用此方法，则会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
