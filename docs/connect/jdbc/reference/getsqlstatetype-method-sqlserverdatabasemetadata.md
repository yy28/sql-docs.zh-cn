---
title: "getSQLStateType 方法 (SQLServerDatabaseMetaData) |Microsoft 文档"
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
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6395cf4f457983cb7ac2540522deea5da93d9b78
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示 SQLException.getSQLState 方法返回的 SQLSTATE 为 X/Open（现称为 Open Group）、SQL CLI、SQL99 (JDBC 3.0) 还是 SQL:2003 (JDBC 4.0)。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**指示 SQLSTATE，类型可以是下列值之一：  
  
-   有关 Java Runtime Environment 版本 5.0： 如果**xopenStates**连接属性设置为**true**，此方法返回 DatabaseMetaData.sqlStateXOpen。 否则为 DatabaseMetaData.sqlStateSQL99。  
  
-   Java Runtime Environment 版本 6.0 的： 如果**xopenStates**连接属性设置为**true**，此方法返回 DatabaseMetaData.sqlStateXOpen。 否则为 DatabaseMetaData.sqlStateSQL。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.DatabaseMetaData 接口中的 getSQLStateType 方法指定此 getSQLStateType 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

