---
title: "setObject 方法 (SQLServerPreparedStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93a2b22c-82b4-48c7-a428-369ebe98a372
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4582f5f5ea56938562570a1b5e01393fa77de76a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-sqlserverpreparedstatement"></a>setObject 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定对象设置指定参数的值。  
  
 开头[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，此方法的行为来修改**sendTimeAsDatetime**连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>重载列表  
  
|Name|Description|  
|----------|-----------------|  
|[setObject （int、 java.lang.Object）](../../../connect/jdbc/reference/setobject-method-int-java-lang-object.md)|使用给定对象设置指定参数的值。|  
|[setObject （int、 java.lang.Object、 int）](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int.md)|使用给定的对象和目标类型的设置指定的参数的值。|  
|[setObject （int、 java.lang.Object、 int、 int）](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int-int.md)|通过使用给定的对象、 目标类型和缩放设置指定的参数的值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

