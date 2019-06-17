---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d6d755283bddca91661907da5a0709cc71c9368
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767123"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 返回的值**enablePrepareOnFirstPreparedStatementCall**连接属性。 如果为 false，第一次执行将调用 sp_executesql 并不准备的语句后第二次执行发生，它将调用 sp_prepexec 并实际设置已准备的语句句柄。 按照执行将调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。 可以通过调用 setDefaultEnablePrepareOnFirstPreparedStatementCall() 更改此选项的默认值。

## <a name="syntax"></a>语法  
  
```  
  
public boolean getEnablePrepareOnFirstPreparedStatementCall()  
```  

## <a name="return-value"></a>返回值
 一个**布尔**，其中包含的值**enablePrepareOnFirstPreparedStatementCall**连接属性。

## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 此方法是可从 JDBC driver 6.4 及前向。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
