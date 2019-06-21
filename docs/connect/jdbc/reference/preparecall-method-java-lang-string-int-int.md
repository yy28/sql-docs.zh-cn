---
title: prepareCall 方法 (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 79340619e65fdcfd0bb076697ef6fa63cfb45c03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771091"
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall 方法 (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象，该对象使用给定的类型和并发机制生成 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
 resultSetType   
  
 指示结果集类型的 int  。  
  
 resultSetConcurrency   
  
 指示结果集并发类型的 int  。  
  
## <a name="return-value"></a>返回值  
 一个 CallableStatement 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 prepareCall 方法由 java.sql.Connection 接口中的 prepareCall 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [prepareCall 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
