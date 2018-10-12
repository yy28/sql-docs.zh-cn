---
title: executeUpdate 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83e035d659fd7b6b59c7b8d8a0799415bef5c112
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611703"
---
# <a name="executeupdate-method-javalangstring-javalangstring"></a>executeUpdate 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行给定的 SQL 语句并向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 发出信号，指示给定数组中指示的自动生成的键应对检索可用。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 一个**字符串**，其中包含 SQL 语句。  
  
 *columnNames*  
  
 一个 String 类型的数组，指示哪些自动生成的键的列名应可用。  
  
## <a name="return-value"></a>返回值  
 指示受影响行数的 int，如果使用 DDL 语句，则此值为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 executeUpdate 方法是由 java.sql.Statement 接口中的 executeUpdate 方法指定的。  
  
 如果执行存储过程将产生大于 1 的更新计数，或生成多个结果集，则请使用 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法执行存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [executeUpdate 方法 (SQLServerStatement)](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
