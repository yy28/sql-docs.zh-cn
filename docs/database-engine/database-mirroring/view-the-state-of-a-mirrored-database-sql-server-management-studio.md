---
title: 查看镜像数据库的状态 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e0bdfdc0f78cda06af9b44a313c82c5f97e4b2fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>查看镜像数据库的状态 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在数据库镜像会话期间，可以在 **“数据库属性”** 对话框的 **“镜像”** 页查看数据库镜像会话的状态。  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>查看数据库镜像会话的状态  
  
1.  连接到主体服务器实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，再选择要镜像的数据库。  
  
3.  右键单击数据库，选择 **“任务”**，再单击 **“镜像”**。 这样便可打开 **“数据库属性”** 对话框的 **“镜像”** 页。  
  
4.  镜像开始后， **“状态”** 窗格将显示您选择 **“镜像”** 页或单击 **“刷新”** 按钮时的数据库镜像会话的状态。 可能的状态如下：  
  
    |状态|解释|  
    |------------|-----------------|  
    |\<blank>|不存在数据库镜像会话，并且没有要在 **“镜像”** 页上报告的活动。|  
    |已暂停|主体数据库正在运行，但没有向镜像服务器发送任何日志。 数据库的镜像副本不可用。|  
    |无连接|主体服务器实例无法连接到其伙伴实例或见证服务器实例（如果存在）|  
    |正在同步|镜像数据库的内容滞后于主体数据库的内容。 主体服务器实例正在向镜像服务器实例发送日志记录，这会对镜像数据库应用更改，使其前滚。<br /><br /> 在数据库镜像会话开始时，镜像数据库和主体数据库处于同步状态。|  
    |故障转移|在主体服务器实例上，手动故障转移（角色切换）已经开始，但镜像服务器实例尚未接受。|  
    |已同步|镜像数据库包含的数据与主体数据库相同。 只有在同步状态下，才能进行手动和自动故障转移。 |  
  
## <a name="see-also"></a>另请参阅  
 [镜像状态 (SQL Server)](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
  
