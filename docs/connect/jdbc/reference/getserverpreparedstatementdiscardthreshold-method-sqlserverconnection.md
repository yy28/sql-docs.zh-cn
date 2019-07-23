---
title: getServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87d7f85799524e3ac7c0e4d99608ce1d82b8f2fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979928"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 返回**serverPreparedStatementDiscardThreshold**连接属性的值。 此设置控制在执行在服务器上清除未完成的句柄之前, 每个连接可以完成多少个未完成的已准备语句放弃操作 (sp_unprepare)。 如果设置为 < = 1, 则在预定义的语句关闭时将立即执行 unprepare 操作。 如果将其设置为 > 1, 则这些调用将一起分批, 以避免调用 sp_unprepare 的开销过于频繁。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold () 来更改此选项的默认值。

## <a name="syntax"></a>语法  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>返回值
 一个**int** , 其中包含**serverPreparedStatementDiscardThreshold**连接属性的值。

## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 此方法可从 JDBC 驱动程序版本6.4 和更前版本获得。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
