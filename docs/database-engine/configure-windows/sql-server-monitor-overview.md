---
title: SQL Server 监视器概述 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 8e53116f762763daac818ff52ae38b0f3841c55b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66775457"
---
# <a name="sql-server-monitor-overview"></a>SQL Server 监视器概述
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 监视器不执行监视功能，但它可以承载执行此功能的模块。 SQL Server 监视器模块包括复制监视器和数据库镜像监视器。  
  
 若要使用其中的一个模块，请在 **“转到”** 菜单上选择该模块。 当前选择的模块拥有导航窗格和详细信息窗格的内容、详细信息窗格中的用户交互以及对内容和状态的查询。  
  
> [!NOTE]  
>  有关这些监视器的详细信息，请参阅 [监视复制](../../relational-databases/replication/monitor/monitoring-replication.md) 和 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)。  
  
## <a name="permissions"></a>权限  
  
-   复制监视器  
  
     若要监视复制，您必须是分发服务器上 **sysadmin** 固定服务器角色的成员，或者是分发数据库中 **replmonitor** 固定数据库角色的成员。 系统管理员可以将任何用户添加到 **replmonitor** 角色中，这样该用户就可以在复制监视器中查看复制活动，但不能管理复制。  
  
-   数据库镜像监视器  
  
     若要监视数据库镜像，必须是服务器实例中 **sysadmin** 固定服务器角色的成员或 **dbm_monitor** 固定数据库角色的成员。 如果你只是某一个伙伴服务器实例中的 **sysadmin** 或 **dbm_monitor** 的成员，则监视器只能连接到该伙伴；监视器不能从其他伙伴中检索信息。 有关详细信息，请参阅 [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md)。  
  
## <a name="menu-options"></a>菜单选项  
 SQL Server 监视器有一个菜单，其中包括用于 SQL Server 监视器的命令。 该菜单中还包括来自选定模块的命令。  
  
 以下菜单选项适用于 SQL Server 监视器。  
  
 **File**  
 此菜单包含“退出”  命令。  
  
 **操作**  
 包含在导航树中所选节点的上下文菜单。  
  
 **“转到”**  
 包含监视组件的列表：  
  
-   数据库镜像  
  
-   复制  
  
 **使用 SQL Server Management Studio 监视数据库镜像**  
  
-   [启动数据库镜像监视器 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
