---
title: "setTime 方法 (SQLServerCallableStatement) |Microsoft 文档"
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
apiname: SQLServerCallableStatement.setTime
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 04ea83b2-db5e-4b46-b016-9e496363827e
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f987cb9ef199c8bcd1d673ae13ff13d38f21821a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="settime-method-sqlservercallablestatement"></a>setTime 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的时间值。  
  
 开头[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，此方法的行为来修改**sendTimeAsDatetime**连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>重载列表  
  
|Name|Description|  
|----------|-----------------|  
|[setTime （java.lang.String，java.sql.Time）](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time.md)|将指定参数设置为给定的时间值。|  
|[setTime （java.lang.String、 java.sql.Time、 java.util.Calendar）](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time-java-util-calendar.md)|将指定参数设置为给定的时间和日历值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 方法](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
