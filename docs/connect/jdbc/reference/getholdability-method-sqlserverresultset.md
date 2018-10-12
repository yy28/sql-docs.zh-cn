---
title: getHoldability 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cf27049e45c8e52c8a63a419327f377dd1f558f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47841395"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的可保持性。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>返回值  
 包含下列可保持性级别之一的 int 值：  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getHoldability 方法由 java.sql.ResultSet 接口中的 getHoldability 方法指定。  
  
 若要设置结果集可保持性，应用程序可使用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 类的 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法。 调用 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) 方法、创建语句对象及其结果集对象并执行该语句后，应用程序可能需要再次更改可保持性。  
  
 对于服务器游标，当连接到 SQL Server 2005 或更高版本时，设置可保持性只会影响该连接上将要创建的新结果集的可保持性。 但是，如果使用 SQL Server 2000，设置可保持性会影响该连接上现有的结果集和将要创建的新结果集的可保持性。  
  
 当重置可保持性和对调用 getHoldability 方法以前创建的结果集对象，此方法返回的值可能不同于通过以下方法返回的可保持性值：Statement.getResultSetHoldabilityConnection.getHoldability 或 DatabaseMetaData.getResultSetHoldability。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
