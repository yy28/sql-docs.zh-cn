---
title: setLockTimeout 方法 (SQLServerDataSource) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 32f61572dca7124e552a9d40497a3385bc243b31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790467"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>setLockTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  设置一个 int  值，指示在数据库报告锁定超时之前要等待的毫秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>Parameters  
 *lockTimeout*  
  
 包含要等待的毫秒数的 int  值。  
  
## <a name="remarks"></a>Remarks  
 锁定超时是指在等待多少毫秒后数据库报告锁定超时。默认值 -1 表示无限期等待。 如果指定，该值将成为此连接上所有语句的默认值。  
  
> [!NOTE]  
>  值为 0 表示不等待。 如果未设置 lockTimeout 属性，[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) 方法将返回默认值 -1。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
