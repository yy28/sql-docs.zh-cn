---
title: "getLockTimeout 方法 (SQLServerDataSource) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.getLockTimeout
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6134888c8c4d2ef9c499e2423e9b14acccbbf91b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>getLockTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回**int**值，该值指示数据库将报告锁定超时之前等待的毫秒数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>返回值  
 **Int**包含的数据库将等待的毫秒数的值。  
  
## <a name="remarks"></a>注释  
 锁定超时值是数据库报告锁定超时之前要等待的毫秒数。默认值 -1 表示可以无限期等待。 如果指定，则此值将为连接上的所有语句的默认值。  
  
> [!NOTE]  
>  值为 0 表示不等待。 如果未设置 lockTimeout 属性，getLockTimeout 方法将返回默认值 -1。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
