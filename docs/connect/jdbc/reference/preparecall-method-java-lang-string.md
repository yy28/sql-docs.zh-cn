---
title: prepareCall 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb83b567-4ce5-447a-93cc-895d4eaf3a05
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 22dd6c5c559dc58b5c381cabc23210e3eade266f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762451"
---
# <a name="preparecall-method-javalangstring"></a>prepareCall 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建用于调用数据库存储过程的 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sql*  
  
 包含 SQL 语句的 String  。  
  
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
  
  
