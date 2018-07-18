---
title: 配置时区-分析平台系统 |Microsoft 文档
description: 时区页上，可在你分析平台系统 (AP) 的设备上设置的所有节点的时间区域。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544651"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>设备时区配置-分析平台系统
**时区**页使你可以在分析平台系统 (AP) 设备上设置的所有节点的时间区域。  
  
## <a name="to-set-the-time-zone"></a>若要设置时区  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  通过停止设备服务**服务状态**页中配置管理器。 请参阅[PDW 服务状态&#40;Analytics Platform System&#41; ](pdw-services-status.md)有关的说明。  
  
3.  在配置管理器的左窗格中，单击**时区**。 选择从所需的时间区域**时区**下拉菜单。 具体取决于你的位置，你可能还选择旁边选中框**自动调整夏令时时钟**。  
  
4.  单击**应用**以保存所做的更改。  
  
5.  通过使用设备启服务**服务状态**页中配置管理器。 如果还打算更改的权限，你可以执行该操作之前重新启动设备。  
  
![DWConfig 设备时间](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另请参阅  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
  
