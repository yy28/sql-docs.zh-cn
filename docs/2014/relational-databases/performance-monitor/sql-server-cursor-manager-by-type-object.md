---
title: SQL Server - Cursor Manager by Type 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0dfe45d6072146d30f13b5f204bad36443d0a54e
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43819933"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server Cursor Manager by Type 对象
  **SQLServer:Cursor Manager by Type** 对象提供计数器（按类型分组）来监视游标。  
  
 此表介绍了 SQL Server **Cursor Manager by Type** 计数器。  
  
|Cursor Manager by Type 计数器|Description|  
|-------------------------------------|-----------------|  
|**Active cursors**|活动游标数。|  
|**Cache Hit Ratio**|高速缓存命中次数和查找次数的比率。|  
|**Cached Cursor Counts**|缓存中给定类型的游标数。|  
|**Cursor Cache Use Count/sec**|每种缓存的游标的使用次数。|  
|**Cursor memory usage**|游标占用的内存量 (KB)。|  
|**Cursor Requests/sec**|服务器收到的 SQL 游标请求数。|  
|**Cursor worktable usage**|游标使用的工作表数。|  
|**Number of active cursor plans**|游标计划数。|  
  
 对象中的每个计数器均包含以下实例：  
  
|Cursor Manager 实例|Description|  
|-----------------------------|-----------------|  
|**_Total**|所有游标的信息。|  
|**API 游标**|仅 API 游标信息。|  
|**TSQL 全局游标**|仅 [!INCLUDE[tsql](../../includes/tsql-md.md)] 全局游标信息。|  
|**TSQL 局部游标**|仅 [!INCLUDE[tsql](../../includes/tsql-md.md)] 局部游标信息。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
