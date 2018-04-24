---
title: 确定失败的群集节点的分析平台系统 |Microsoft 文档
description: 本文介绍如何确定失败发生群集故障转移后引发了群集故障转移警报分析平台系统 (AP) 节点的名称。 作为故障排除群集故障转移的一部分，你必须确定联系 Microsoft 以帮助解决此问题之前失败的节点的名称。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 031c8033e91d7a7f74ca8c4409bc02296a22ebcf
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>确定哪些群集节点失败分析平台系统
本主题介绍如何确定失败发生群集故障转移后引发了群集故障转移警报分析平台系统 (AP) 节点的名称。 作为故障排除群集故障转移的一部分，你必须确定联系 Microsoft 以帮助解决此问题之前失败的节点的名称。  
  
## <a name="Background"></a>背景  
为 SQL Server PDW 中的高可用性，管理节点和计算节点被配置为 Windows 故障转移群集的主动或被动组件。 当一个活动的服务器失败时对关键系统请求作出响应时，被动服务器故障转移，并执行该故障服务器的功能。  
  
群集故障转移后，当 SQL Server PDW 报告节点状态被动服务器都有故障状态。 但是，它是不明显哪个服务器或节点失败，尤其是故障的服务器上仍处于联机状态。 若要解决了群集失败，必须确定故障转移的节点的名称。  
  
## <a name="AdminConsoleSolution"></a>管理员控制台解决方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要查找失败的节点名称  
  
1.  打开管理控制台。 管理员控制台的详细信息，请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 发生故障转移后，在故障转移事件包含中的警报数上**运行状况**页。 没有**运行状况**页，则为 PDW 区域 HDI 区域中，以及设备的构造区域。 每个运行状况页具有**警报**选项卡。若要了解有关警报的详细信息，单击运行状况页中，警报选项卡，然后单击警报。  
  
## <a name="SystemView"></a>系统视图解决方案  
以下 SQL 语句演示如何使用[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)系统视图来查找该故障服务器的名称。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
