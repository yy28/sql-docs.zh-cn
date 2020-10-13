---
title: SQL Server 实用工具的功能和任务 | Microsoft Docs
description: 熟悉 SQL Server 实用工具。 了解其功能以及如何使用它来监视 SQL Server 环境。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9f37e62285ffcd3623bd1a26609466556e07634c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810413"
---
# <a name="sql-server-utility-features-and-tasks"></a>SQL Server 实用工具的功能和任务
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户具有作为一个整体管理其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境的要求，在此版本中通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中的应用程序和多服务器管理概念满足了这一要求。  
  
## <a name="benefits-of-the-sql-server-utility"></a>SQL Server 实用工具的优点  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具在一个统一的视图中对组织的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相关实体进行建模。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSMS) 中的实用工具资源管理器和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实用工具视点通过用作实用工具控制点 (UCP) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例向管理员提供反映 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源运行状况的整体视图。 通过在 UCP 中为使用过度和使用不足策略以及多种重要参数提供的摘要和详细数据的组合，可以实现资源合并机会，并且能够轻松发现资源使用过度的情况。 运行状况策略是可以配置的，并且可以进行调整以便更改资源使用率阈值的上限和下限。 可以更改全局监视策略，或为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中管理的每个实体配置单独的监视策略。  
  
##  <a name="getting-started-with-sql-server-utility"></a><a name="typical_scenarios"></a> SQL Server 实用工具入门  
 一般的用户方案都是从创建实用工具控制点开始，该实用工具控制点为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具建立中心原因点。 该 UCP 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中提供从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例收集的资源运行状况的合并视图。 在创建该 UCP 后，您将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中，以便该 UCP 可以管理它们。  
  
 可基于全局策略定义或者基于单独的策略定义监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个实例和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具管理的数据层应用程序。  
  
## <a name="related-tasks"></a>Related Tasks  
 参考以下主题可以开始使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具。  
  
|说明|主题|  
|-|-|  
|介绍配置服务器以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的同一实例中运行实用工具和非实用工具收集组时的注意事项。|[在 SQL Server 的同一实例中运行实用工具和非实用工具收集组的注意事项](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|介绍如何创建 SQL Server 实用工具控制点。|[创建 SQL Server 实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|介绍如何连接到 SQL Server 实用工具。|[连接到 SQL Server 实用工具](../../relational-databases/manage/connect-to-a-sql-server-utility.md)|  
|介绍如何向实用程序控制点注册 SQL Server 实例。|[注册 SQL Server 实例（SQL Server 实用工具）](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|介绍如何使用实用工具资源管理器来管理 SQL Server 实用工具。|[使用实用工具资源管理器管理 SQL Server 实用工具](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|介绍如何在 SQL Server 实用工具中监视 SQL Server 实例。|[在 SQL Server 实用工具中监视 SQL Server 的实例](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|介绍如何查看资源运行状况策略结果。|[查看资源运行状况策略结果（SQL Server 实用工具）](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)|  
|介绍如何修改资源运行状况策略定义。|[修改资源运行状况策略定义（SQL Server 实用工具）](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|介绍如何配置 UCP 数据仓库。|[配置实用工具控制点数据仓库（SQL Server 实用工具）](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|介绍如何配置实用工具运行状况策略。|[配置运行状况策略（SQL Server 实用工具）](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)|  
|介绍如何调整 CPU 使用策略的分布。|[减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|介绍如何从 UCP 删除 SQL Server 实例。|[从 SQL Server 实用工具中删除 SQL Server 实例](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|介绍如何在 SQL Server 的托管实例上更改实用工具数据收集器的代理帐户。|[在 SQL Server 的托管实例上更改实用工具收集组的代理帐户（SQL Server 实用工具）](../../relational-databases/manage/change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|介绍如何在 SQL Server 的实例之间移动 UCP。|[将 UCP 从 SQL Server 的一个实例移到另一个实例（SQL Server 实用工具）](../../relational-databases/manage/move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|介绍如何删除 UCP。|[删除实用工具控制点（SQL Server 实用工具）](../../relational-databases/manage/remove-a-utility-control-point-sql-server-utility.md)|  
|介绍如何排除 SQL Server 实用工具的故障。|[SQL Server 实用工具故障排除](/previous-versions/sql/sql-server-2016/ee210592(v=sql.130))|  
|介绍如何排除 SQL Server 资源运行状况的故障。|[SQL Server 资源运行状况故障排除（SQL Server 实用工具）](../../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|指向 UtilityExplorer F1 帮助主题的链接。|[实用工具资源管理器的 F1 帮助](../../relational-databases/manage/utility-explorer-f1-help.md)|  
  
