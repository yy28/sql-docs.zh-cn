---
description: execute 方法 (java.lang.String)
title: execute 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.execute (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a871917e-d286-46c3-96cf-2e8e8b22111c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0375eb9dd2d9252ed914fa554beb54faa7e345ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437749"
---
# <a name="execute-method-javalangstring"></a>execute 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行可返回多个结果的给定的 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>参数  
 *sql*  
  
 包含 SQL 语句的 String****。  
  
## <a name="return-value"></a>返回值  
 如果语句返回结果集，则值为 true****。 如果它返回更新计数或不返回任何结果，则值为 false****。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此执行方法是由 java.sql.Statement 接口中的执行方法指定的。  
  
 此方法替代 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 类中的 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法。  
  
 调用此方法将导致异常，因为在创建 SQLServerPreparedStatement 对象时指定了该对象的 SQL 语句。  
  
## <a name="see-also"></a>另请参阅  
 [execute 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
