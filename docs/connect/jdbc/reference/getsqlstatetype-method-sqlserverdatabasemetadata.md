---
title: getSQLStateType 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 55079e30c2f8908153cc708aca699e77aef41261
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66774177"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示 SQLException.getSQLState 方法返回的 SQLSTATE 为 X/Open（现称为 Open Group）、SQL CLI、SQL99 (JDBC 3.0) 还是 SQL:2003 (JDBC 4.0)。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>返回值  
 指示 SQLSTATE 类型的 int  ，可以为以下值之一：  
  
-   对于 5.0 版的 Java 运行时环境： 如果**xopenStates**连接属性设置为**true**，此方法返回 DatabaseMetaData.sqlStateXOpen。 否则，返回的是 DatabaseMetaData.sqlStateSQL99。  
  
-   对于 6.0 版的 Java 运行时环境： 如果**xopenStates**连接属性设置为**true**，此方法返回 DatabaseMetaData.sqlStateXOpen。 否则为 DatabaseMetaData.sqlStateSQL。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSQLStateType 方法由 java.sql.DatabaseMetaData 接口中的 getSQLStateType 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
