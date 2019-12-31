---
title: 配置时区
description: "\"时区\" 页面使你可以为分析平台系统（AP）设备上的所有节点设置时区。"
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401394"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>设备时区配置-分析平台系统
"**时区**" 页面使你可以为分析平台系统（ap）设备上的所有节点设置时区。  
  
## <a name="to-set-the-time-zone"></a>设置时区  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)。  
  
2.  使用 Configuration Manager 中的 "**服务状态**" 页停止设备服务。 有关说明，请参阅[PDW 服务状态 &#40;分析平台系统&#41;](pdw-services-status.md) 。  
  
3.  在 Configuration Manager 的左窗格中 **，单击 "时区"**。 从 **"时区**" 下拉菜单中选择所需的时区。 根据您的位置，您还可以选择 "**自动调整夏令时的时钟**" 旁边的复选框。  
  
4.  单击 "**应用**" 以保存所做的更改。  
  
5.  使用 Configuration Manager 中的 "**服务状态**" 页重新启动设备服务。 如果还计划更改权限，可以在重新启动设备之前执行此操作。  
  
![DWConfig 工具时间](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另请参阅  
[启动 Configuration Manager &#40;Analytics 平台系统&#41;](launch-the-configuration-manager.md)  
  
