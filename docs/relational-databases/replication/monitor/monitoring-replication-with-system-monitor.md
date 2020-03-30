---
title: 使用系统监视器监视复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 91db0303326c74b710e7755de5a9573539e61425
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68082982"
---
# <a name="monitoring-replication-with-system-monitor"></a>使用系统监视器监视复制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通过使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 系统监视器，您可以使用图形、图表和报告来测量计算机的效率，确定并解决可能的问题（如资源使用不平衡、硬件不足或程序设计有问题等），以及针对其他硬件需求制定计划。 有关详细信息，请参阅[监视资源使用情况（系统监视器）](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)。  
  
 系统监视器使用性能对象和计数器，它们提供各种进程的性能信息。 您可以通过与复制代理相关联的计数器来测量复制的性能：  
  
|代理|性能对象|计数器|说明|  
|-----------|------------------------|-------------|-----------------|  
|所有代理|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：复制代理|正在运行|当前正在运行的复制代理数。|  
|快照代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：复制快照|Snapshot:Delivered Cmds/sec|每秒传递到分发服务器的命令数。|  
|快照代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：复制快照|Snapshot:Delivered Trans/sec|每秒传递到分发服务器的事务数。|  
|日志读取器代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Logreader|Logreader:Delivered Cmds/sec|每秒传递到分发服务器的命令数。|  
|日志读取器代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Logreader|Logreader:Delivered Trans/sec|每秒传递到分发服务器的事务数。|  
|日志读取器代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Logreader|Logreader:Delivery Latency|从事务应用于发布服务器起，到传递给分发服务器为止所经过的时间（以毫秒为单位）。|  
|分发代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Dist.|Dist:Delivered Cmds/sec|每秒传递到订阅服务器的命令数。|  
|分发代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Dist.|Dist:Delivered Trans/sec|每秒传递到订阅服务器的事务数。|  
|分发代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：Replication Dist.|Dist:Delivery Latency|从事务传递给分发服务器起，到应用于订阅服务器为止所经过的时间（以毫秒为单位）。|  
|合并代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：复制合并|Conflicts/sec|在合并过程中每秒出现的冲突数。|  
|合并代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：复制合并|Downloaded Changes/sec|每秒从发布服务器复制到订阅服务器的行数。|  
|合并代理|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]设置用户帐户 ：复制合并|Uploaded Changes/sec|每秒从订阅服务器复制到发布服务器的行数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视（复制）](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
