---
title: getHoldability 方法 (SQLServerResultSet) |Microsoft 文档
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
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2143d3487e4a3ec28c9577f55819dc0240ca3854
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此保持能力[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**值，该值包含以下保持能力级别之一：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 getHoldability 方法指定此 getHoldability 方法。  
  
 若要设置结果集保持能力，应用程序可以使用[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)类。 后[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)方法调用和创建语句对象和其结果集对象和执行该语句时，应用程序可能需要再次更改保持能力。  
  
 对于服务器游标时连接到 SQL Server 2005 或更高版本，将设置保持能力影响仅是还将创建在该连接上的新结果集的保持能力。 但是，如果使用 SQL Server 2000，设置保持能力会影响该连接上现有的结果集和将要创建的新结果集的保持能力。  
  
 如果重置保持能力并且 getHoldability 方法调用以前创建的结果集的对象，此方法返回的值可能不同于通过以下方法返回的保持能力值： Statement.getResultSetHoldabilityConnection.getHoldability 或 DatabaseMetaData.getResultSetHoldability。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
