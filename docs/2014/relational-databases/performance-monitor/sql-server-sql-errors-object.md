---
title: SQL Server - SQL Errors 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5a35d9dcb9564c4081d008768c28e28dd1f7c1e6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066897"
---
# <a name="sql-server-sql-errors-object"></a>SQL Server SQL Errors 对象
  Microsoft **中的** SQLServer:SQL Errors [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象提供了一些计数器，以监视 **SQL Errors**。  
  
 下表介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL 错误计数器  。  
  
|SQL Server SQL Errors 计数器|说明|  
|------------------------------------|-----------------|  
|**Errors/sec**|每秒的错误数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|Item|定义|  
|----------|----------------|  
|**_Total**|有关所有错误的信息。|  
|**DB 离线错误**|跟踪导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将当前数据库离线的错误。|  
|**信息错误**|与错误消息相关的信息，错误消息可向用户提供信息但不会导致错误。|  
|**断开连接错误**|跟踪导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 断开当前连接的错误。|  
|**用户错误**|有关用户错误的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
