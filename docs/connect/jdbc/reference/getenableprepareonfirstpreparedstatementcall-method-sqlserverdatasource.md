---
title: getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 721e19f1a4941cacfd18e04a14e6fa6d851cde60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667514"
---
# <a name="getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource"></a>getEnablePrepareOnFirstPreparedStatementCall 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回的值**enablePrepareOnFirstPreparedStatementCall**连接属性。 如果此配置，则返回 false 首次执行的已准备的语句将调用 sp_executesql 并不准备语句，它将调用 sp_prepexec 并实际安装程序已准备的语句句柄，会发生第二次执行后。 按照执行将调用 sp_execute。 如果该语句仅执行一次，这关闭使 sp_unprepare 已准备的语句上的需要。 
  
## <a name="syntax"></a>语法  
  
```
public boolean getEnablePrepareOnFirstPreparedStatementCall();  
```  
  
## <a name="return-value"></a>返回值  
 返回**布尔**的值**enablePrepareOnFirstPreparedStatementCall**连接属性。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 此方法是可从 JDBC driver 6.4 及前向。
 
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
