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
manager: craigg
ms.openlocfilehash: dd78992abf04f78bb7b8fe879d030e906568588c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638686"
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
  
  
