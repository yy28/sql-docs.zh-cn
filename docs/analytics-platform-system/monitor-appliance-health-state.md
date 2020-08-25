---
title: 监视设备运行状况
description: 如何使用管理控制台或直接查询并行数据仓库动态管理视图来监视分析平台系统设备的状态。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400990"
---
# <a name="monitor-appliance-health-state"></a>监视设备运行状况状态
本文介绍如何使用管理控制台或直接查询并行数据仓库动态管理视图来监视分析平台系统设备的状态。 
  
## <a name="to-monitor-the-appliance-state"></a>监视设备状态  
系统管理员可以使用管理控制台或 SQL Server PDW 的动态管理视图 (Dmv) 检索节点、组件和软件的完整层次结构。 下图简要了解了 SQL Server PDW 监视的组件。  
  
![监视概述](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>使用管理控制台监视组件状态  
使用管理控制台检索组件状态：  
  
1.  单击 " **设备状态** " 选项卡。  
  
2.  在 "设备状态" 页上，单击特定节点以查看节点详细信息。  
  
    ![PDW 管理控制台状态](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>使用系统视图监视组件状态  
若要使用系统视图检索组件状态，请使用 [sys. dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。 例如，以下查询将检索所有组件的状态。  
  
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
  
为 Status 属性返回的可能值为：  
  
-   正常  
  
-   非关键  
  
-   严重  
  
-   未知  
  
-   不支持  
  
-   不可访问  
  
-   无法恢复  
  
若要查看所有组件的所有属性，请删除 `WHERE  p.property_name = 'Status'` 子句。  
  
**[Update_time]** 列显示 SQL Server PDW health 代理上次轮询组件的时间。  
  
> [!CAUTION]  
> 请务必调查组件未轮询5分钟或更长时间时的问题;可能会出现指示软件检测信号问题的警报。  
  
## <a name="see-also"></a>另请参阅  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[设备监视 &#40;分析平台系统&#41;](appliance-monitoring.md)  
  
