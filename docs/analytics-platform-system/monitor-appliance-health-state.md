---
title: 监视设备运行状况-分析平台系统
description: 如何通过使用管理控制台中，或通过直接查询的并行数据仓库动态管理视图监视分析平台系统设备的状态。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d8616d291dcaa8afadc01c9bd237903ca6c13573
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-appliance-health-state"></a>监视器设备运行状况状态
此文章介绍了如何通过使用管理控制台中，或通过直接查询的并行数据仓库动态管理视图监视分析平台系统设备的状态。 
  
## <a name="to-monitor-the-appliance-state"></a>若要监视设备状态  
系统管理员可以使用管理控制台或 SQL Server PDW 动态管理视图 (Dmv) 来检索的节点、 组件和软件的完整层次结构。 下图提供了 SQL Server PDW 监视的组件较高级别的了解。  
  
![监视概述](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>通过使用管理控制台的监视组件状态  
若要使用管理控制台检索组件状态：  
  
1.  单击**装置状态更改为**选项卡。  
  
2.  在设备状态页上，单击以查看节点详细信息的特定节点上。  
  
    ![PDW 管理员控制台状态](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>通过使用系统视图的监视组件状态  
若要通过使用系统视图检索组件状态，请使用[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。 例如，以下查询检索的所有组件的状态。  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
可能的状态属性返回的值为：  
  
-   还行  
  
-   非关键  
  
-   严重  
  
-   Unknown  
  
-   不支持  
  
-   无法访问  
  
-   无法恢复  
  
若要查看的所有组件的所有属性，请删除`WHERE  p.property_name = 'Status'`子句。  
  
**[Update_time]**列将显示该组件已轮询的 SQL Server PDW 运行状况代理的最后一个时间。  
  
> [!CAUTION]  
> 请务必调查该问题，当组件 5 分钟或更长时间; 不已对轮询可能表明软件检测信号出现问题的警报。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备监视&#40;分析平台系统&#41;](appliance-monitoring.md)  
  
