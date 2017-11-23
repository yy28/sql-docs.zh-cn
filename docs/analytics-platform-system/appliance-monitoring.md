---
title: "设备监视 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 253864fb-9178-41d2-a0ae-5dd9fd0a4fda
caps.latest.revision: "25"
ms.openlocfilehash: dbbae960d5e4d88b6cb725c9e22fc36a428b9264
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-monitoring"></a>设备监视
本设备监视指南介绍的工具和用于监视 SQL Server PDW 设备的任务。  
  
## <a name="Basics"></a>监视基础知识和工具  
值和在 SQL Server PDW 设备上可以监视的信息还是很多。 例如，以下是典型监视任务。  
  
-   检查 SQL Server PDW 由颁发任何警报。  
  
-   有关故障的硬件的监视器。  
  
-   监视的网络连接问题。  
  
-   检查查询处理过程中返回给用户的错误。  
  
-   查看当前活动会话和查询的数量。  
  
-   检查加载、 备份和还原的状态。  
  
### <a name="appliance-monitoring-tools"></a>设备监视工具  
有多个工具可用于监视设备。  
  
管理控制台  
SQL Server PDW 具有管理控制台。 这是一个显示有关查询、 加载、 备份和还原、 锁、 会话、 警报和设备状态的信息的基于 web 的工具。 在设备; 上运行的管理控制台用户连接到 Internet 资源管理器通过管理控制台。 有关详细信息，请参阅：  
  
-   [使用管理控制台 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理控制台警报](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系统视图  
SQL Server PDW 包括使你能够获取有关设备运行状况、 状态和性能的详细的信息的综合系统视图。 有关的监视任务的系统视图的列表，请参阅：  
  
-   [使用系统视图 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW 具有大量与 Systems Center Operations Manager 的集成。 SQL Server PDW 的管理包都可用作免费下载。 有关使用 System Center 来监视 SQL Server PDW 的详细信息，请参阅以下资源：  
  
-   [使用 System Center Operations Manager &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自定义解决方案  
情况下 System Center 与监视工具，你数据中心不可用时你可以监视设备通过使用第三方监视解决方案。 在 PDW，当前不支持的外部软件代理的安装，但大多数监视解决方案支持 Transact\-SQL 集成，以便系统管理员可以实现直接 Transact\-针对你 PDW 的 SQL 查询设备。  
  
如果你的监视解决方案不支持直接 Transact\-SQL 查询，或者你没有监视工具，则可以使用脚本来执行监视任务，例如发生警报时发送电子邮件。  TechNet wiki 包含已编写脚本的监视解决方案示例。  
  
-   [监视 SQL Server PDW 示例的 power Shell](http://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>相关监视任务  
  
|监视任务|Description|  
|-------------------|---------------|  
|通过使用管理控制台监视设备。|[使用管理控制台 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|通过使用系统视图来监视设备。|[使用系统视图 &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 监视设备|[使用 System Center Operations Manager &#40; 监视设备分析平台系统 &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|监视的设备的状态。|[监视器设备运行状况状态 &#40;分析平台系统 &#41;](monitor-appliance-health-state.md)|  
|检测信号监视。|[将遥测反馈发送到 Microsoft &#40;SQL Server PDW &#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|跟踪设备警报。|[跟踪设备警报 &#40;分析平台系统 &#41;](track-appliance-alerts.md)|  
|确定正在使用多少容量。|[查看容量使用率 &#40;分析平台系统 &#41;](view-capacity-utilization.md)|  
|确定如何通常进行轮询设备。|[确定轮询频率 &#40;分析平台系统 &#41;](determine-polling-frequency.md)|  
|当发生群集故障时，确定哪些群集节点失败。|[确定群集节点故障 &#40;分析平台系统 &#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备管理任务 &#40;分析平台系统 &#41;](appliance-management-tasks.md)  
  
