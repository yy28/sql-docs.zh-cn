---
description: setUser 方法 (SQLServerDataSource)
title: setUser 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b887e5b0af5d4a91a8cbea2b3676fd958ac3c077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472170"
---
# <a name="setuser-method-sqlserverdatasource"></a>setUser 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置用于连接数据源的用户名。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>参数  
 *user*  
  
 一个包含用户名的字符串****。  
  
## <a name="remarks"></a>注解  
 setUser 方法设置将用于连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用户名。 如果未设置用户名值，[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) 方法则返回默认值 Null。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
