---
title: execute 方法 (java.lang.String) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d3ffb7c175c21d56467899bba9de7c110e324d1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802345"
---
# <a name="execute-method-javalangstring"></a>execute 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行可返回多个结果的给定的 SQL 语句。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final boolean execute(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
## <a name="return-value"></a>返回值  
 **true**如果语句返回结果集。 **false**如果返回更新计数或无结果。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此执行方法是由 java.sql.Statement 接口中的执行方法指定的。  
  
 此方法替代 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 类中的 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法。  
  
 调用此方法将导致异常，因为在创建 SQLServerPreparedStatement 对象时指定了该对象的 SQL 语句。  
  
## <a name="see-also"></a>另请参阅  
 [execute 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
