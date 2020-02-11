---
title: 确定失败的群集节点
description: 本文介绍如何在发生群集故障转移并引发群集故障转移警报后，确定失败的分析平台系统（AP）节点的名称。 在排查群集故障转移过程中，必须先确定失败节点的名称，然后联系 Microsoft 以帮助解决问题。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401200"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>确定分析平台系统的群集节点失败
本主题介绍如何确定在发生群集故障转移并引发群集故障转移警报后失败的分析平台系统（AP）节点的名称。 在排查群集故障转移过程中，必须先确定失败节点的名称，然后联系 Microsoft 以帮助解决问题。  
  
## <a name="Background"></a>背景  
为了 SQL Server PDW 中的高可用性，控制节点和计算节点配置为 Windows 故障转移群集的主动或被动组件。 当活动服务器无法响应关键系统请求时，被动服务器将进行故障转移，并执行失败的服务器的功能。  
  
群集故障转移后，当 SQL Server PDW 报告节点状态时，被动服务器的状态为 "已故障转移"。 但这并不明显是哪个服务器或节点发生故障，尤其是故障服务器仍处于联机状态时。 若要排查群集故障，必须确定已进行故障转移的节点的名称。  
  
## <a name="AdminConsoleSolution"></a>管理控制台解决方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>查找失败的节点的名称  
  
1.  打开管理控制台。 有关管理控制台的详细信息，请参阅[使用管理控制台监视设备 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 发生故障转移后，故障转移事件会包含在 "**运行状况**" 页上的警报数中。 对于该设备，有一个 "PDW" 区域和 "结构" 区域的**运行状况**页面。 每个运行状况页面都有一个 "**警报**" 选项卡。若要了解有关警报的详细信息，请单击 "运行状况" 页和 "警报" 选项卡，然后单击 "警报"。  
  
## <a name="SystemView"></a>系统视图解决方案  
下面的 SQL 语句演示如何使用[sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)系统视图查找失败的服务器的名称。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
