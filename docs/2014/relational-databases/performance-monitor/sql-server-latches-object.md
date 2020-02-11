---
title: SQL Server - Latches 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d0d9249a5cfb801e07a85132060bb4d1781346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63251103"
---
# <a name="sql-server-latches-object"></a>SQL Server Latches 对象
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的**SQLServer：闩锁**对象提供计数器，用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]监视称为闩锁的内部资源锁。 通过监视闩锁来确定用户活动和资源使用情况，将有助于查明性能瓶颈。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Latches** 计数器。  
  
|SQL Server Latches 计数器|说明|  
|---------------------------------|-----------------|  
|**平均闩锁等待时间（毫秒）**|必须等待授予的闩锁请求的平均等待时间（毫秒）。|  
|**闩锁等待数/秒**|未能立即授予的闩锁请求数。|  
|**Superlatch 数**|目前是 SuperLatch 的闩锁数。|  
|**SuperLatch 降级数/秒**|在上一秒钟内已降级为常规闩锁的 SuperLatch 数。|  
|**SuperLatch 促销/秒**|在上一秒钟内已提升为 SuperLatch 的闩锁数。|  
|**总闩锁等待时间（毫秒）**|上一秒钟内的闩锁请求的总等待时间（毫秒）。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
