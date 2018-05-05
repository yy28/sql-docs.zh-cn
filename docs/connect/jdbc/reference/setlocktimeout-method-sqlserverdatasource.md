---
title: setLockTimeout 方法 (SQLServerDataSource) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d59acf61221284480c349b38206737bea6499af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>setLockTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  集**int**值，该值指示在数据库报告锁定超时之前要等待的毫秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>Parameters  
 *lockTimeout*  
  
 **Int**值，该值包含要等待的毫秒数。  
  
## <a name="remarks"></a>注释  
 锁定超时值是数据库报告锁定超时之前要等待的毫秒数。默认值 -1 表示可以无限期等待。 如果指定，则此值将为连接上的所有语句的默认值。  
  
> [!NOTE]  
>  值为 0 表示不等待。 如果未设置 lockTimeout 属性， [getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)方法返回-1 的默认值。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
