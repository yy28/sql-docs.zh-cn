---
title: refreshRow 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19bd400492ba8ce8547f48b83b2f94544bd28a2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812615"
---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用数据库中当前行的最新值刷新此行。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 refreshRow 方法由 java.sql.ResultSet 接口中的 refreshRow 方法指定。  
  
 游标位于插入行时，无法调用此方法。  
  
 此方法为应用程序提供了显式告知 JDBC 驱动程序从数据库重新提取行的方法。 当 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 缓存或预提取，以从数据库提取行的最新值时，应用程序可能需要调用此方法。 如果提取大小大于 1，则 JDBC 驱动程序可能实际上同时刷新多行。  
  
 重新提取所有值将受事务隔离级别和游标敏感性的制约。 如果调用 updater 方法后，但在调用 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法前调用此方法，则会丢失对行所做的更新。 频繁地调用此方法可能会降低性能。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
