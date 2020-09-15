---
description: setLockTimeout 方法 (SQLServerDataSource)
title: setLockTimeout 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37b43e351f2b44ed4376acb60150bca0eed516ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431739"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>setLockTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置一个 int**** 值，指示在数据库报告锁定超时之前要等待的毫秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>参数  
 *lockTimeout*  
  
 包含要等待的毫秒数的 int**** 值。  
  
## <a name="remarks"></a>注解  
 锁定超时是指在等待多少毫秒后数据库报告锁定超时。默认值 -1 表示无限期等待。 如果指定，该值将成为此连接上所有语句的默认值。  
  
> [!NOTE]  
>  值为 0 表示不等待。 如果未设置 lockTimeout 属性，[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) 方法将返回默认值 -1。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
