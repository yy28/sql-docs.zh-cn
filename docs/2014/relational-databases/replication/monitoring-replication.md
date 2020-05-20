---
title: 监视复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 615582b2d961f87a2d3df151175d7bd5d06e305f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000380"
---
# <a name="monitoring-replication"></a>监视（复制）
  监视复制拓扑是部署复制的一个重要方面。 因为复制活动是分布式的，所以跟踪复制过程中涉及的所有计算机的活动和状态非常有必要。 以下工具可用于监视复制：  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)][!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]复制监视器  
  
     复制监视器是监视复制最重要的工具，它可以显示以发布服务器为中心的所有复制活动视图。 有关详细信息，请参阅[通过复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)。  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 提供对复制监视器的访问。 它还允许您查看当前状态以及下列代理所记录的最后一条消息，还允许您启动和停止每个代理：日志读取器代理、快照代理、合并代理和分发代理。 有关详细信息，请参阅 [Monitor Replication Agents](monitor/monitor-replication-agents.md)。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 和复制管理对象 (RMO)  
  
     两个界面都可用于监视分发服务器上的所有复制类型。 合并复制还提供从发布服务器监视复制的功能。  
  
-   复制代理事件的警报  
  
     复制提供了许多复制代理事件的预定义警报，如果有必要，您还可以创建其他警报。 警报用于触发对某个事件的自动响应和/或用于通知管理员。 有关详细信息，请参阅[对复制代理事件使用警报](agents/use-alerts-for-replication-agent-events.md)。  
  
-   系统监视器  
  
     系统监视器对性能监视很有用，它可为复制提供多个计数器。 有关详细信息，请参阅 [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复制管理常见问题](administration/frequently-asked-questions-for-replication-administrators.md)   
 [复制管理的最佳做法](administration/best-practices-for-replication-administration.md)   

  
  
