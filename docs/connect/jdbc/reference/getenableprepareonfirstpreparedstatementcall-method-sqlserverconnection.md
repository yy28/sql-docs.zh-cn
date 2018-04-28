---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
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
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 768da613ce6bf9fd629ff972c80082f00347d6da
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 返回的值**enablePrepareOnFirstPreparedStatementCall**连接属性。 如果为 false 在首次执行将调用 sp_executesql 并做好准备的语句，一旦第二次执行发生它将调用 sp_prepexec 并实际设置的已准备的语句句柄。 以下执行将调用 sp_execute。 如果仅一次执行的语句，这关闭缓解 sp_unprepare 已准备的语句上的需要。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 更改此选项的默认值。

## <a name="syntax"></a>语法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>返回值
 A**布尔**包含值的**enablePrepareOnFirstPreparedStatementCall**连接属性。

## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>注释  
 此方法是从 JDBC 驱动程序版本 6.4 可用且开始。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
