---
title: 查看资源运行状况策略结果（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52137a6405090ca52f3a99f21b400a573e606dc0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775799"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>查看资源运行状况策略结果（SQL Server 实用工具）
  使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中的实用工具仪表板，可以查看 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实用工具资源参数。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](sql-server-utility-features-and-tasks.md)。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>查看 SQL Server 实用工具的资源运行状况策略结果  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (SSMS) 中，单击“视图”，然后单击“实用工具资源管理器”以便查看实用工具资源管理器导航窗格。 若要查看内容窗格，请单击 **“视图”**，然后单击 **“实用工具资源管理器内容”**。  
  
2.  在导航窗格中，单击 ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")“连接到实用工具”。 如果尚未创建实用工具控制点 (UCP)，或者尚未将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例或者数据层应用程序注册到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实用工具中，请参阅 [SQL Server 实用工具功能和任务](sql-server-utility-features-and-tasks.md)。  
  
3.  单击 UCP 节点可以查看 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的摘要数据（右键单击可以刷新）。 面板数据将显示在内容窗格中。  
  
4.  单击“托管实例”节点可以查看 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的托管实例的列表视图数据（右键单击可以刷新）。 列表视图数据将显示在内容窗格中。  
  
5.  单击“已部署的数据层应用程序”节点可查看数据层应用程序的列表视图（右键单击可刷新）。 列表视图数据将显示在内容窗格中。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 实用工具的功能和任务](sql-server-utility-features-and-tasks.md)   
 [减少 CPU 使用策略中的干扰（SQL Server 实用工具）](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [已部署的数据层应用程序详细信息（SQL Server 实用工具）](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [托管实例详细信息（SQL Server 实用工具）](../../database-engine/managed-instance-details-sql-server-utility.md)   
 [实用工具管理（SQL Server 实用工具）](../../database-engine/utility-administration-sql-server-utility.md)  
  
  
