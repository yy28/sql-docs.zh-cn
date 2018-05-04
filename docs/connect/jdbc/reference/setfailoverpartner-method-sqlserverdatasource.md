---
title: setFailoverPartner 方法 (SQLServerDataSource) |Microsoft 文档
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
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf1c29750ef93d131e39616b2cd2d3059c8dd9b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>setFailoverPartner 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置在数据库镜像配置中使用的故障转移服务器的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parameters  
 *ServerName*  
  
 A**字符串**包含故障转移服务器名称。  
  
## <a name="remarks"></a>注释  
 如果在与主服务器进行初始连接时失败，则使用由此方法设置的值；建立初始连接后，将忽略此值。 [SetDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)方法还应该使用结合使用这种方法，否则将引发异常。  
  
 驱动程序不支持在设置故障转移服务器名称时指定故障转移服务器的端口号。 但是，调用[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)方法和[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)方法替换[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)支持方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
