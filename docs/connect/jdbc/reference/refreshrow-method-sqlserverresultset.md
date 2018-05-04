---
title: refreshRow 方法 (SQLServerResultSet) |Microsoft 文档
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
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e35c595f96554af3aea0bd4912b7d2f2bfa8250a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
 由 java.sql.ResultSet 接口中的 refreshRow 方法指定此 refreshRow 方法。  
  
 游标位于插入行时，无法调用此方法。  
  
 此方法为应用程序提供了显式告知 JDBC 驱动程序从数据库重新提取行的方法。 应用程序可能需要调用此方法时[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]缓存或预提取要从数据库中获取行的最新值。 如果提取大小大于 1，则 JDBC 驱动程序可能实际上同时刷新多行。  
  
 重新提取所有值将受事务隔离级别和游标敏感性的制约。 如果在调用 updater 方法，但在调用之前调用此方法[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法，对行进行的更新将会丢失。 频繁地调用此方法可能会降低性能。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
