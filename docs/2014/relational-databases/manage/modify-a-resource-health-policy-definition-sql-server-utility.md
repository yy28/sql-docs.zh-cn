---
title: 修改资源运行状况策略定义（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.UTILITY.ADMINISTRATION.F1
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b489fda1c051ecd08b63f28d6232a0e213d9fcb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793999"
---
# <a name="modify-a-resource-health-policy-definition-sql-server-utility"></a>修改资源运行状况策略定义（SQL Server 实用工具）
  本主题介绍了如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中修改资源使用情况策略定义。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中修改资源使用情况策略之前，必须先创建一个实用工具控制点 (UCP)。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](sql-server-utility-features-and-tasks.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以为数据层应用程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例配置实用工具资源使用情况策略。 可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为所有数据层应用程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例全局定义资源使用情况策略；也可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为每个数据层应用程序和每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例单独定义资源使用情况策略。 您还可以实现全局策略，并且用它们自己的策略定义配置单独的数据层应用程序或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="modify-global-resource-utilization-policies-in-a-sql-server-utility"></a>在 SQL Server 实用工具中修改全局资源使用情况策略。  
  
1.  连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的 UCP。  
  
2.  在实用工具资源管理器导航窗格中，单击 **“实用工具管理”** 以便查看或修改全局监视策略，然后在实用工具资源管理器内容窗格中单击 **“策略”** 选项卡。  
  
3.  在实用工具资源管理器内容窗格中，通过单击箭头或策略说明，选择“设置全局数据层监视策略”或“设置全局托管的实例监视策略”。  
  
4.  使用策略说明右侧的控件可以设置使用过度或使用不足策略阈值。  
  
5.  根据需要使用“应用” 、“放弃” 或“还原默认设置”  按钮。 策略更改可能需要最多 15 分钟的时间，以便传播回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具面板和列表视图详细信息。  
  
6.  若要刷新数据，请在实用工具资源管理器导航窗格中右键单击“实用工具管理”节点，然后选择“刷新”。  
  
#### <a name="modify-resource-health-policy-definitions-for-an-individual-data-tier-application-or-an-individual-managed-instance-of-sql-server-in-a-sql-server-utility"></a>在 SQL Server 实用工具中为单独的数据层应用程序或 SQL Server 的单独托管实例修改资源运行状况策略定义。  
  
1.  连接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 UCP。  
  
2.  在实用工具资源管理器导航窗格中，单击“已部署的数据层应用程序”或者单击“托管实例”，以便查看或修改用于单独数据层应用程序或托管实例的监视策略。  
  
3.  在实用工具资源管理器内容窗格列表视图中，单击数据层应用程序或你要修改其策略的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称，然后单击“策略详细信息”选项卡。  
  
4.  通过单击箭头或策略说明，选择要查看或修改的策略。 默认情况下将选择全局策略。  
  
5.  选择单选按钮“覆盖全局策略”可覆盖全局策略，并为指定的数据层应用程序实现单独的策略定义。  
  
6.  使用策略说明右侧的控件可以设置使用过度或使用不足策略阈值。  
  
7.  根据需要使用“应用” 、“放弃” 或“还原默认设置”  按钮。 策略更改可能需要最多 15 分钟的时间，以便传播回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具面板和列表视图详细信息。  
  
8.  若要刷新数据，请在实用工具资源管理器导航窗格中右键单击“已部署的数据层应用程序”节点，然后选择“刷新”。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具的功能和任务](sql-server-utility-features-and-tasks.md)   
 [查看资源运行状况策略结果（SQL Server 实用工具）](view-resource-health-policy-results-sql-server-utility.md)  
  
  
