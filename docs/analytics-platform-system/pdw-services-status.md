---
title: PDW 服务状态
description: 分析平台系统的并行数据仓库（PDW）服务状态。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400857"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>分析平台系统的并行数据仓库服务状态
Microsoft Analytics Platform System Configuration Manager 中的 "并行数据仓库**服务状态**" 页显示所有 SQL Server PDW 服务的当前状态，并提供停止和启动 PDW 服务的功能。 这是启动和停止 PDW 服务的唯一受支持的方法。 请注意，不能单独启动单个组件或服务。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>启动或停止设备服务  
  
1.  若要启动设备服务，请单击 "**启动设备**"。  
  
2.  若要停止设备服务，请单击 "**停止设备**"。  
  
使用 "**启动设备**" 和 "**停止设备**" 启动和停止设备服务时，不需要单击 "**应用**"。  
  
![DWConfig 工具 PDW 服务](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 停止 PDW 区域还会停止节点上的 PDW 代理（sqldwagent）。 PDW agent 需要 PDW 控制节点来报告运行状况监视。  
  
## <a name="see-also"></a>另请参阅  
[&#40;Analytics Platform System&#41;打开或关闭 AP 设备](power-the-aps-appliance-on-or-off.md)  
  
