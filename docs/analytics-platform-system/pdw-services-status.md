---
title: PDW 服务状态-分析平台系统 |Microsoft Docs
description: 分析平台系统并行数据仓库 (PDW) 的服务状态。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3db994b4869c1b017a079b404af3d95db1316dad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960369"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>分析平台系统的并行数据仓库服务状态
并行数据仓库**服务状态**页在 Microsoft 分析平台系统 Configuration Manager 中显示的当前状态的所有 SQL Server PDW 服务，并提供的功能来停止和启动 PDW 服务。 这是用于启动和停止 PDW 服务唯一受支持的方法。 请注意，单个组件或服务无法启动独立。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>若要启动或停止设备服务  
  
1.  若要启动设备服务，请单击**启动设备**。  
  
2.  若要停止设备服务，请单击**停止设备**。  
  
没有必要单击**Apply**启动或停止使用的工具服务时**启动设备**并**停止设备**。  
  
![DWConfig 工具 PDW 服务](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> 在节点上停止 PDW 区域也停止 PDW 代理 (sqldwagent)。 PDW 代理需要 PDW 控制节点，以报告运行状况监视。  
  
## <a name="see-also"></a>请参阅  
[打开或关闭电源 APS 设备&#40;分析平台系统&#41;](power-the-aps-appliance-on-or-off.md)  
  
