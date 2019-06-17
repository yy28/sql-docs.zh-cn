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
manager: jroth
ms.openlocfilehash: 22f7bf637d20b42a7dadd3397e84c826fa277a22
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791923"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 返回的值**serverPreparedStatementDiscardThreshold**连接属性。 此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 如果设置为 < = 1，撤消已准备的语句关闭上立即执行操作。 如果设置为 > 1，这些调用会放在一起以避免过于频繁调用 sp_unprepare 的开销。 可以通过调用 getDefaultServerPreparedStatementDiscardThreshold() 更改此选项的默认值。

## <a name="syntax"></a>语法  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>返回值
 **Int** ，其中包含的值**serverPreparedStatementDiscardThreshold**连接属性。

## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 此方法是可从 JDBC driver 6.4 及前向。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
