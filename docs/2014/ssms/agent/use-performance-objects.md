---
title: 使用性能对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ccba43aa28cadef1995fab001f66e1f4bebacde
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245853"
---
# <a name="use-performance-objects"></a>使用性能对象
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理包括用于监视服务执行情况的性能对象和计数器。 这些性能对象使您可以使用性能监视器（一个 Windows 工具）来识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务在后台的运行情况。 例如，您可以通过识别 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务当前运行的活动作业数量来找出那些锁定的作业。  
  
 计算机上安装的每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例都拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务性能对象和计数器。 性能对象是根据每个对象所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例来命名的。  
  
 下表显示了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务性能对象的命名方式：  
  
|实例类型|对象名称|  
|-------------------|-----------------|  
|默认|**SQLAgent：对象** **：计数器**|  
|已命名|**SQLAgent$**<br /> ***instance_name* ：** *对象*：*计数器*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的下列性能对象。  
  
|对象名称|说明|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|已启动作业的相关性能信息、成功率和当前状态|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|作业步骤的相关状态信息|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警报和通知数的相关信息|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|常规性能信息|  
  
## <a name="see-also"></a>另请参阅  
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [启动系统监视器 (Windows)](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
