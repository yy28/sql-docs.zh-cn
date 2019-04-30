---
title: 确定失败的群集节点的分析平台系统 |Microsoft Docs
description: 本文介绍如何确定失败发生群集故障转移并引发了群集故障转移警报后 Analytics Platform System (APS) 节点的名称。 作为故障排除群集故障转移的一部分，必须确定联系 Microsoft 以帮助解决此问题之前失败的节点的名称。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4fd739e55725a3138a22539ef837088f86c8d8b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283148"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>确定哪个群集节点的分析平台系统失败
本主题介绍如何确定失败发生群集故障转移并引发了群集故障转移警报后 Analytics Platform System (APS) 节点的名称。 作为故障排除群集故障转移的一部分，必须确定联系 Microsoft 以帮助解决此问题之前失败的节点的名称。  
  
## <a name="Background"></a>背景  
为 SQL Server PDW 中的高可用性，控制节点和计算节点配置为 Windows 故障转移群集的主动或被动组件。 当活动的服务器无法对关键系统请求做出响应时，则被动服务器故障转移，并且执行失败的服务器的功能。  
  
群集故障转移时，SQL Server PDW 节点状态报告时被动服务器后故障转移状态。 但是，它不明显的服务器或节点失败，尤其是故障的服务器上仍处于联机状态。 若要排查群集故障，必须确定故障转移节点的名称。  
  
## <a name="AdminConsoleSolution"></a>管理员控制台解决方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要查找失败的节点的名称  
  
1.  打开管理控制台。 有关在管理控制台的详细信息，请参阅[通过使用管理控制台监视设备&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 发生故障转移后，故障转移事件包含在警报数量上**运行状况**页。 没有**运行状况**页面，PDW 区域并在设备的 fabric 区域。 每个运行状况页具有**警报**选项卡。若要了解有关警报的详细信息，请单击运行状况页，警报选项卡，然后单击警报。  
  
## <a name="SystemView"></a>系统视图解决方案  
以下 SQL 语句演示如何使用[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)系统视图来查找失败的服务器的名称。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
