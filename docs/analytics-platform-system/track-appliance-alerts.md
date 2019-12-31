---
title: 跟踪设备警报
description: 在分析平台系统中跟踪设备警报。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399945"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>在分析平台系统中跟踪设备警报
本主题说明如何使用管理控制台和系统视图来跟踪 SQL Server PDW 设备中的警报。  
  
## <a name="to-track-appliance-alerts"></a>跟踪设备警报  
SQL Server PDW 会为需要注意的硬件和软件问题创建警报。 每个警报都包含问题的标题和描述。  
  
SQL Server PDW 在[sys. dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV 中记录警报。 系统将保留超过10000个警报的限制，并在超出限制时首先删除最早的警报。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>使用管理控制台查看警报  
对于 PDW 区域和设备的结构区域，有一个 "**警报**" 选项卡。 发生故障转移后，故障转移事件包含在页面上的警报数中。 对于该设备，有一个适用于 PDW 区域和结构区域的页面。 每个运行状况页面都有一个选项卡。若要了解有关警报的详细信息，请单击 "**运行状况**" 页和 "**警报**" 选项卡，然后单击 "警报"。  
  
![PDW 管理控制台警报](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
在 "**警报**" 页上：  
  
-   若要查看警报历史记录，请单击 "**查看警报历史记录**" 链接。  
  
-   若要查看警报组件及其当前属性值，请单击 "警报" 行。  
  
-   若要查看有关引发警报的节点的详细信息，请单击节点名称。  
  
### <a name="view-alerts-by-using-the-system-views"></a>使用系统视图查看警报  
若要通过使用系统视图查看警报，请查询[sys.databases. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)。 此 DMV 显示尚未更正的警报。 有关会审警报和错误的帮助，请使用[sys. dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV。  
  
下面的示例是一个查看当前警报的常见查询。  
  
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
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[设备监视 &#40;分析平台系统&#41;](appliance-monitoring.md)  
  
