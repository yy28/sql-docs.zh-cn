---
title: prepareStatement 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0db2871-3a5f-4fcc-af61-92333042dcd1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 26c783fdf58b9614623fb8a73d3298b222f45563
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802672"
---
# <a name="preparestatement-method-javalangstring-javalangstring"></a>prepareStatement 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建用于将参数化的 SQL 语句发送到数据库的 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
 columnNames   
  
 一个**字符串**列名称的数组。  
  
## <a name="return-value"></a>返回值  
 一个 PreparedStatement 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 prepareStatement 方法由 java.sql.Connection 接口中的 prepareStatement 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [prepareStatement 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
