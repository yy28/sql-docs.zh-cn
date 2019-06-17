---
title: getWarnings 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 15af39bf-6285-44cc-a021-7341e7a055c4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f816cab36fbed46dbf25c83df3063a024e4abbbb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780075"
---
# <a name="getwarnings-method-sqlserverconnection"></a>getWarnings 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索调用此 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 对象时报告的第一个警告。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>返回值  
 一个 SQLWarning 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getWarnings 方法由 java.sql.Connection 接口中的 getWarnings 方法指定。  
  
 后续的警告都是链接到第一个 SQLWarning，与 getNextWarning 方法调用。 如果在关闭的连接上调用，将引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
