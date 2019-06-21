---
title: setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eddf7b58456a4730ff783ab4f53a9911da06d8db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782966"
---
# <a name="setserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>setServerPreparedStatementDiscardThreshold 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 指定特定的连接实例的行为。 此设置控制多少未完成准备语句丢弃之前执行调用以清理服务器上未完成的句柄，则可以每个连接未完成操作 (sp_unprepare)。 当设置为 < = 1 取消-准备关闭已准备的语句上立即执行操作。 如果值设置为 > 1 这些调用会一起批处理，以避免过于频繁调用 sp_unprepare 的开销。


## <a name="syntax"></a>语法  
  
```  
  
public void setServerPreparedStatementDiscardThreshold(boolean thresholdValue)  
```  

#### <a name="parameters"></a>Parameters  
 thresholdValue   
 
 新值**serverPreparedStatementDiscardThreshold**连接属性。  
 
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 此方法是可从 JDBC driver 6.4 及前向。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
