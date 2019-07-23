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
ms.openlocfilehash: 76faa3bcaccac4f75d95dc49276c669a5631b5a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979730"
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
  
-   对于 Java Runtime Environment 版本 5.0: 如果将**xopenStates**连接属性设置为**true**, 则此方法将返回 java.sql.databasemetadata。 否则，返回的是 DatabaseMetaData.sqlStateSQL99。  
  
-   对于 Java Runtime Environment 版本 6.0: 如果将**xopenStates**连接属性设置为**true**, 则此方法将返回 java.sql.databasemetadata。 否则为 Java.sql.databasemetadata. sqlStateSQL。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSQLStateType 方法由 getSQLStateType 方法在 Java.sql.databasemetadata 接口中指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
