---
title: 设备监视
description: 此设备监视指南介绍了用于监视分析平台系统设备的工具和任务。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401427"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>分析平台系统的设备监视
此设备监视指南介绍了用于监视分析平台系统设备的工具和任务。  
  
## <a name="monitoring-basics-and-tools"></a><a name="Basics"></a>监视基础知识和工具  
可在 SQL Server PDW 设备上监视的值和信息广泛。 例如，下面是典型的监视任务。  
  
-   检查 SQL Server PDW 发出的任何警报。  
  
-   监视故障的硬件。  
  
-   监视网络连接问题。  
  
-   检查在查询处理期间返回给用户的错误。  
  
-   查看当前活动会话和查询的数量。  
  
-   检查加载、备份和还原的状态。  
  
### <a name="appliance-monitoring-tools"></a>设备监视工具  
有多种工具可用于监视设备。  
  
管理控制台  
SQL Server PDW 具有管理控制台。 这是一种基于 web 的工具，用于显示有关查询、加载、备份和还原、锁、会话、警报和设备状态的信息。 管理控制台在设备上运行;用户通过 Internet Explorer 连接到管理控制台。 有关详细信息，请参见:  
  
-   [使用管理控制台 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理控制台警报](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系统视图  
SQL Server PDW 包括可让你获取有关设备运行状况、状态和性能的详细信息的全面系统视图。 有关监视任务的系统视图的列表，请参阅：  
  
-   [使用系统视图 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW 与系统中心 Operations Manager 的广泛集成。 SQL Server PDW 的管理包可免费下载。 有关使用 System Center 监视 SQL Server PDW 的详细信息，请参阅以下内容：  
  
-   [使用 System Center Operations Manager &#40;Analytics 平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自定义解决方案  
对于你的数据中心监视工具无法使用 System Center 的情况，你可以通过使用第三方监视解决方案来监视该设备。 PDW 目前不支持安装外部软件代理，但大多数监视解决方案支持 Transact-sql\-集成，因此，系统管理员可以对 PDW 设备实施直接的 transact-sql\-查询。  
  
如果你的监视解决方案不支持直接执行\-SQL 查询，或者你没有监视工具，则可以使用脚本来执行监视任务，如在出现警报时发送电子邮件。  TechNet wiki 包含一个脚本化监视解决方案示例。  
  
-   [SQL Server PDW 的 Power Shell 监视示例](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="related-monitoring-tasks"></a><a name="Tasks"></a>相关监视任务  
  
|监视任务|说明|  
|-------------------|---------------|  
|使用管理控制台监视设备。|[使用管理控制台 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|使用系统视图监视设备。|[使用系统视图 &#40;分析平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 监视设备|[使用 System Center Operations Manager &#40;Analytics 平台系统来监视设备&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|监视设备的状态。|[监视设备运行状况状态 &#40;分析平台系统&#41;](monitor-appliance-health-state.md)|  
|检测信号监视。|[将遥测反馈发送给 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|跟踪设备警报。|[&#40;分析平台系统跟踪设备警报&#41;](track-appliance-alerts.md)|  
|确定使用的容量。|[查看 &#40;Analytics Platform System&#41;的容量利用率](view-capacity-utilization.md)|  
|确定轮询设备的频率。|[&#40;分析平台系统&#41;确定轮询频率](determine-polling-frequency.md)|  
|发生群集故障时，确定哪个群集节点发生故障。|[确定哪些群集节点 &#40;分析平台系统失败&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[&#40;Analytics Platform System&#41;的设备管理任务](appliance-management-tasks.md)  
  
