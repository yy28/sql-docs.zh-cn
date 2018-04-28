---
title: setObject 方法 （int、 java.lang.Object） |Microsoft 文档
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
ms.topic: article
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ddb600d1b034359263c2a84286bd752e4e6d859d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="setobject-method-int-javalangobject"></a>setObject 方法 (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用给定对象设置指定参数的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parameters  
 *索引*  
  
 **Int** ，该值指示参数号。  
  
 *obj*  
  
 一个对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setObject 方法指定此 setObject 方法。  
  
 调用此 setObject 方法之前，应用程序可能通过使用以下方法之一设置指定的参数：  
  
-   集\<类型 > SQLServerPreparedStatement 类或 SQLServerCallableStatement 类的方法  
  
-   SQLServerPreparedStatement 类或 SQLServerCallableStatement 类的 setNull 方法  
  
-   [RegisterOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 类的方法  
  
 在这种情况下，将自动设置参数的类型。 如果应用程序将调用具有 obj 值 NULL 此 setObject 方法，该驱动程序假定参数的类型是一个设置的以前调用的方法。  
  
 如果 obj 值为 NULL，并且可以确定该参数无类型信息，此 setObject 方法将发送到数据库之前将指定的参数转换为字符上。  
  
 开头[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0，此方法的行为来修改**sendTimeAsDatetime**连接属性 ([设置连接属性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 有关详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setObject 方法&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
