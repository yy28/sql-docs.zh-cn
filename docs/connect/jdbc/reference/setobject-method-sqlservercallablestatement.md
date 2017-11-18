---
title: "setObject 方法 (SQLServerCallableStatement) |Microsoft 文档"
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
- SQLServerCallableStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b1b11d4929f14543c6930021284c55e9bfbffd6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-sqlservercallablestatement"></a>setObject 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置使用给定的对象的指定参数的值。  
  
 开头[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，此方法的行为来修改**sendTimeAsDatetime**连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>重载列表  
  
|Name|Description|  
|----------|-----------------|  
|[setObject （java.lang.String，java.lang.Object）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|设置使用给定的对象的指定参数的值。|  
|[setObject （java.lang.String、 java.lang.Object、 int）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|使用给定的对象和目标类型设置指定参数的值。|  
|[setObject （java.lang.String、 java.lang.Object、 int、 int）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|使用给定的对象、目标类型和小数位数设置指定参数的值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

