---
title: 跟踪设备警报-分析平台系统 |Microsoft Docs
description: 跟踪分析平台系统中的设备警报。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 62f116b8e45512d5a6fc5ce50c0fbc76344103be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960025"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>跟踪分析平台系统中的设备警报
本主题说明如何使用管理控制台和系统视图来跟踪 SQL Server PDW 设备中的警报。  
  
## <a name="to-track-appliance-alerts"></a>若要跟踪设备警报  
SQL Server PDW 创建需要注意的硬件和软件问题的警报。 每个警报包含标题和问题的说明。  
  
SQL Server PDW 中日志警报[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV。 系统保留的限制为 10,000 的警报，并当超出限制时，首先删除最旧的警报。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>通过使用管理控制台查看警报  
没有**警报**选项卡的 PDW 区域以及设备的 fabric 区域。 发生故障转移后，故障转移事件将包括在页面上的警报数量。 没有页面的 PDW 区域以及设备的 fabric 区域。 每个运行状况页都有一个选项卡。若要了解有关警报的详细信息，请单击**运行状况**页上，**警报**卡，并单击警报。  
  
![PDW 管理控制台警报](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
上**警报**页：  
  
-   若要查看警报历史记录，请单击**查看警报历史记录**链接。  
  
-   若要查看警报的组件和它的当前属性值，请单击警报的行。  
  
-   若要查看有关引发警报的节点的详细信息，请单击节点名称。  
  
### <a name="view-alerts-by-using-the-system-views"></a>通过使用系统视图查看警报  
若要使用系统视图查看警报，请查询[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)。 此 DMV 显示未更正的警报。 会审警报和错误的帮助，请使用[sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV。  
  
下面的示例是用于查看当前警报的常用查询。  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[设备监视&#40;分析平台系统&#41;](appliance-monitoring.md)  
  
