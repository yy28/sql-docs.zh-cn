---
title: "prepareCall 方法 （java.lang.String、 int、 int、 int） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67154127b6428a0b41960b6b822c3e727d6224f5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall 方法 (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)对象，它生成[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)具有给定的类型、 并发和保持能力的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 A**字符串**包含 SQL 语句。  
  
 *nType*  
  
 **Int** ，该值指示结果集类型。  
  
 *nConcur*  
  
 **Int** ，该值指示结果集并发类型。  
  
 *nHold*  
  
 **Int** ，该值指示结果集保持能力。  
  
## <a name="return-value"></a>返回值  
 一个 CallableStatement 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Connection 接口中的 prepareCall 方法指定此 prepareCall 方法。  
  
## <a name="see-also"></a>另请参阅  
 [prepareCall 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
