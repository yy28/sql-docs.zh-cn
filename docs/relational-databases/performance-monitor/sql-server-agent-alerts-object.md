---
title: SQL Server 代理 - Alerts 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d55a1cb1e918dde94862202de0fa54aed5ff4d54
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158505"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server 代理中的 Alerts 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 代理中的 **Alerts** 性能对象包含性能计数器，可报告有关 SQL Server 代理警报的信息。 下表列出了此对象包含的计数器。  
  
 下表介绍了 **SQLAgent:Alerts** 计数器。  
  
|“属性”|描述|  
|----------|-----------------|  
|**Activated alerts**|此计数器可报告自上次 SQL Server 代理重新启动以来 SQL Server 代理已经激活的警报总数。|  
|**Alerts activated/minute**|此计数器可报告上一分钟内 SQL Server 代理激活的警报数。|  
  
> [!NOTE]  
>  用户必须是 **sysadmin** 固定服务器角色的成员，才能使用此 SQL Server 代理对象。  
  
## <a name="see-also"></a>另请参阅  
 [Alerts](../../ssms/agent/alerts.md)   
 [使用性能对象](../../ssms/agent/use-performance-objects.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
