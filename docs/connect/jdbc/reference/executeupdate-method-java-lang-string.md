---
title: executeUpdate 方法 (java.lang.String，int[]) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff53657ab4e5bd99fb41cc2c01ce18add3e78b46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785685"
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 方法 (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行给定的 SQL 语句，并向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 发出信号，指示给定数组中自动生成的键都应可用于检索。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 一个**字符串**，其中包含 SQL 语句。  
  
 *columnIndexes*  
  
 一个整数数组，指示应可用的自动生成的键的列索引。  
  
## <a name="return-value"></a>返回值  
 一个指示受影响的行数的 int，如果使用 DDL 语句，则为 0。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 executeUpdate 方法是由 java.sql.Statement 接口中的 executeUpdate 方法指定的。  
  
 如果执行存储过程将产生大于 1 的更新计数，或生成多个结果集，则请使用 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法执行存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [executeUpdate 方法 (SQLServerStatement)](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
