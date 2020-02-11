---
title: 监视作业活动 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6310453e1257aaee1a02f035c7213ef4fe6131af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62704774"
---
# <a name="monitor-job-activity"></a>监视作业活动
  可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业活动监视器监视在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中定义的所有作业的当前活动。  
  
## <a name="sql-server-agent-sessions"></a>SQL Server 代理会话  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每次启动服务时，代理都会创建一个新会话。 创建新会话后，将用所有现有已定义的作业填充 **msdb** 数据库中的 **sysjobactivity** 表。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理重新启动时，此表将保留作业的上一次活动。 每个会话均记录从作业开始到作业结束的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的正常作业活动。 有关这些会话的信息存储在 **msdb** 数据库的 **syssessions** 表中。  
  
## <a name="job-activity-monitor"></a>作业活动监视器  
 作业活动监视器允许使用 **查看** sysjobactivity [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]表。 您可以查看服务器上的所有作业，或定义筛选器以限制显示的作业数。 还可以通过单击“代理作业活动”**** 网格中的某个列标题来对作业信息进行排序。 例如，当选择“上次运行时间”**** 列标题时，可以按上次运行的顺序查看作业。 多次单击列标题可使作业按照上次运行的日期在升序和降序之间切换。  
  
 使用作业活动监视器，可以执行下列任务：  
  
-   启动和停止作业。  
  
-   查看作业属性。  
  
-   查看特定作业的历史。  
  
-   手动刷新“代理作业活动”**** 网格中的信息，或者通过单击“查看刷新设置”**** 设置自动刷新间隔。  
  
 若要查看计划运行的作业、当前会话期间运行的作业的最新结果以及当前正在运行或空闲的作业，请使用作业活动监视器。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务意外失败，您可以参考作业活动监视器中的上一次会话来确定正在执行的作业。  
  
 若要打开作业活动监视器，请在 ** 对象资源管理器中展开“SQL Server 代理”**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，右键单击“作业活动监视器”****，再单击“查看作业活动”****。  
  
 也可以使用存储过程 **sp_help_jobactivity**查看当前会话的作业活动。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**说明**|**主题**|  
|介绍如何查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的运行时状态。|[View Job Activity](view-job-activity.md)|  
  
## <a name="see-also"></a>另请参阅  
 [查看作业活动](view-job-activity.md)   
 [sysjobactivity &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobactivity-transact-sql)   
 [syssessions &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-syssessions-transact-sql)   
 [sp_help_jobactivity &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql)  
  
  
