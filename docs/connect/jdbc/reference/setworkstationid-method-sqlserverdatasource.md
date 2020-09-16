---
description: setWorkstationID 方法 (SQLServerDataSource)
title: setWorkstationID 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 435116e862cc973230928d444c2c67e3c6bbf973
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450580"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接数据源的客户端计算机名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>参数  
 *workstationID*  
  
 包含客户端计算机名称的 String****。  
  
## <a name="remarks"></a>注解  
 workstationID 是客户端计算机或工作站的名称。 如果未设置 workstationID 属性，则通过调用 InetAddress.getLocalHost().getHostName() 方法构造默认值。 如果 getHostName 返回空值，则调用 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
