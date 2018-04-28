---
title: executeUpdate 方法 (java.lang.String、 int[]) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fb2372d8ae0da672430c2817a29a6c440b0817a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 方法 (java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行给定的 SQL 语句和信号[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]指示给定的数组中的自动生成密钥应该进行检索。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 A**字符串**包含 SQL 语句。  
  
 *columnIndexes*  
  
 一个整数数组，指示应可用的自动生成的键的列索引。  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示行受影响，则为 0 的数，如果使用的 DDL 语句。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 executeUpdate 方法指定此 executeUpdate 方法。  
  
 如果执行存储的过程结果中的更新计数大于 1，或生成多个结果集，使用[执行](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法来执行存储的过程。  
  
## <a name="see-also"></a>另请参阅  
 [executeUpdate 方法&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
