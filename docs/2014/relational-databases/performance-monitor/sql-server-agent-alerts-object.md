---
title: SQL Server 代理 - Alerts 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d81d7ba399799caba4f8b58cf6b69baeab033a5a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37184249"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server 代理中的 Alerts 对象
  SQL Server 代理中的 **Alerts** 性能对象包含性能计数器，可报告有关 SQL Server 代理警报的信息。 下表列出了此对象包含的计数器。  
  
 下表介绍了 **SQLAgent:Alerts** 计数器。  
  
|“属性”|Description|  
|----------|-----------------|  
|**Activated alerts**|此计数器可报告自上次 SQL Server 代理重新启动以来 SQL Server 代理已经激活的警报总数。|  
|**Alerts activated/minute**|此计数器可报告上一分钟内 SQL Server 代理激活的警报数。|  
  
> [!NOTE]  
>  用户必须是 **sysadmin** 固定服务器角色的成员，才能使用此 SQL Server 代理对象。  
  
## <a name="see-also"></a>请参阅  
 [Alerts](../../ssms/agent/alerts.md)   
 [使用性能对象](../../ssms/agent/use-performance-objects.md)   
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
