---
title: 监视设备的分析平台系统 |Microsoft Docs
description: 此设备监视指南介绍的工具和监视 Analytics Platform System 设备的任务。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 100a587814e62a6455d25e78a3defca973f39bf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276143"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>设备监视 Analytics Platform system
此设备监视指南介绍的工具和监视 Analytics Platform System 设备的任务。  
  
## <a name="Basics"></a>监视基础知识和工具  
值和 SQL Server PDW 设备上可以监视的信息还是很多。 例如，以下是典型监视任务。  
  
-   检查 SQL Server PDW 发出任何警报。  
  
-   监视的故障的硬件。  
  
-   监视的网络连接问题。  
  
-   检查查询处理期间返回给用户的错误。  
  
-   查看当前处于活动状态的会话和查询的数目。  
  
-   检查加载、 备份和还原的状态。  
  
### <a name="appliance-monitoring-tools"></a>设备监视工具  
有多个工具可用于监视设备。  
  
管理员控制台  
SQL Server PDW 有管理员控制台。 这是一个基于 web 的工具来显示有关查询、 加载、 备份和还原、 锁、 会话、 警报和设备状态信息。 在管理控制台上设备; 运行用户连接到 Internet 资源管理器通过在管理控制台。 有关详细信息，请参阅：  
  
-   [通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理控制台警报](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系统视图  
SQL Server PDW 包括使你能够获取有关设备运行状况、 状态和性能的详细的信息的综合系统视图。 系统视图的监视任务的列表，请参阅：  
  
-   [使用系统视图监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW 具有与 Systems Center Operations Manager 的丰富集成。 可免费下载 SQL Server PDW 的管理包。 如何使用 System Center 监视 SQL Server PDW 的详细信息，请参阅：  
  
-   [使用 System Center Operations Manager 监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自定义解决方案  
情况下 System Center 与监视工具，你的数据中心不可用时你可以监视设备使用第三方监视解决方案。 中，当前不支持外部软件代理的安装，但大多数监视解决方案支持 Transact\-SQL 集成，以便系统管理员可以实现直接 Transact\-保持 PDW 针对的 SQL 查询设备。  
  
如果监视解决方案不支持直接 Transact\-SQL 查询，或你不具有一个监视工具，则可以使用脚本来执行监视任务，例如发生警报时发送电子邮件。  TechNet wiki 包含已编写脚本的监视解决方案示例。  
  
-   [Power Shell 适用于 SQL Server PDW 监视示例](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>相关的监视任务  
  
|监视任务|Description|  
|-------------------|---------------|  
|通过使用管理控制台监视设备。|[通过使用管理控制台监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|使用系统视图监视设备。|[使用系统视图监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 监视设备|[使用 System Center Operations Manager 监视设备&#40;分析平台系统&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|监视设备的状态。|[监视设备运行状况&#40;分析平台系统&#41;](monitor-appliance-health-state.md)|  
|检测信号监视。|[向 Microsoft 发送遥测反馈&#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|跟踪设备警报。|[跟踪设备警报&#40;分析平台系统&#41;](track-appliance-alerts.md)|  
|确定正在使用多少容量。|[查看容量利用率&#40;分析平台系统&#41;](view-capacity-utilization.md)|  
|确定通常轮询设备的方式。|[确定轮询频率&#40;分析平台系统&#41;](determine-polling-frequency.md)|  
|群集故障时，确定哪个群集节点失败。|[确定哪个群集节点失败&#40;分析平台系统&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备管理任务&#40;分析平台系统&#41;](appliance-management-tasks.md)  
  
