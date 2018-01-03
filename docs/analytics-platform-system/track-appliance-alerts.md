---
title: "跟踪设备警报 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 631345d9-4967-461a-8922-e5f8fd33f48f
caps.latest.revision: "14"
ms.openlocfilehash: a780aa34667280d9e079dad4f44954ba919275d5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="track-appliance-alerts"></a>跟踪设备警报
本主题说明如何使用管理控制台和系统视图来跟踪在 SQL Server PDW 设备中的警报。  
  
## <a name="to-track-appliance-alerts"></a>若要跟踪设备警报  
SQL Server PDW 创建需要关注的硬件和软件问题的警报。 每个警报包含标题和问题的说明。  
  
SQL Server PDW 中记录警报[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV。 系统保留的限制为 10,000 的警报，并当超出限制时，首先删除最旧的警报。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>通过使用管理控制台查看警报  
没有**警报**选项卡上，则为 PDW 区域 HDI 区域中，并构造区域的设备。 发生故障转移后，在故障转移事件将包括在页面上的警报的数目。 没有，则为 PDW 区域 HDI 区域中，和设备的构造区域的页。 每个运行状况页都有一个选项卡。若要了解有关警报的详细信息，请单击**运行状况**页上，**警报**选项卡上，然后单击警报。  
  
![PDW 管理控制台警报](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
上**警报**页：  
  
-   若要查看的警报的历史记录，请单击**查看警报历史记录**链接。  
  
-   若要查看的警报的组件，并且其当前的属性值，请单击警报的行。  
  
-   若要查看有关引发警报的节点的详细信息，请单击节点名称。  
  
### <a name="view-alerts-by-using-the-system-views"></a>通过使用系统视图查看警报  
若要通过使用系统视图查看警报，查询[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)。 此 DMV 显示未更正的警报。 对于会审警报和错误的帮助，请使用[sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV。  
  
下面的示例是用于查看当前警报常见的查询。  
  
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
[设备监视 &#40;分析平台系统 &#41;](appliance-monitoring.md)  
  
