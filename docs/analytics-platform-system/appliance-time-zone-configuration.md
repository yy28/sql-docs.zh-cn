---
title: 设备的时区配置 (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cea9eeb9-fe05-4e65-b229-539de02ab20a
caps.latest.revision: 18
ms.openlocfilehash: cb03dd9b766c92e92b329f1e0c9daedb7cd56703
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="appliance-time-zone-configuration"></a>设备的时区配置
**时区**页使你可以在 SQL Server PDW 设备上设置的所有节点的时间区域。  
  
## <a name="to-set-the-time-zone"></a>若要设置时区  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  通过停止设备服务**服务状态**页中配置管理器。 请参阅[PDW 服务状态&#40;Analytics Platform System&#41; ](pdw-services-status.md)有关的说明。  
  
3.  在配置管理器的左窗格中，单击**时区**。 选择从所需的时间区域**时区**下拉菜单。 具体取决于你的位置，你可能还选择旁边选中框**自动调整夏令时时钟**。  
  
4.  单击**应用**以保存所做的更改。  
  
5.  通过使用设备启服务**服务状态**页中配置管理器。 如果还打算更改的权限，你可以执行该操作之前重新启动设备。  
  
![DWConfig Appliance Time](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>另请参阅  
[启动配置管理器&#40;分析平台系统&#41;](launch-the-configuration-manager.md)  
  
