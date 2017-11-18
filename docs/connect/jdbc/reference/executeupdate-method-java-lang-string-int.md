---
title: "executeUpdate 方法 （java.lang.String，int） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb27e4538eccf87257d16555505442f76461adb0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  运行给定的 SQL 语句和信号[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]有关是否自动生成密钥，给定的标志与生成此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象应变为可供检索。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 A**字符串**包含 SQL 语句。  
  
 *标志*  
  
 **Int**值，该值指示是否应使自动生成的键可用。 它必须是下列常量之一：  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示行受影响，则为 0 的数，如果使用的 DDL 语句。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 executeUpdate 方法指定此 executeUpdate 方法。  
  
 如果执行存储的过程结果中的更新计数大于 1，或生成多个结果集，使用[执行](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法来执行存储的过程。  
  
## <a name="see-also"></a>另请参阅  
 [executeUpdate 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

