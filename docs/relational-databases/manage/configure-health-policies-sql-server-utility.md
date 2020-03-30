---
title: 配置运行状况策略（SQL Server 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c59138d5d1f06ffee0266f9e97d5faf46ef28f08
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115442"
---
# <a name="configure-health-policies-sql-server-utility"></a>配置运行状况策略（SQL Server 实用工具）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 实用工具仪表板，可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具资源参数。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 若要查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具运行状况策略结果，请从 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]连接到实用工具控制点。 有关详细信息，请参阅 [使用实用工具资源管理器来管理 SQL Server 实用工具](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可为数据层应用程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例配置实用工具运行状况策略。 可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为所有数据层应用程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例全局定义运行状况策略；或者，可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中为每个数据层应用程序和每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 托管实例单独定义运行状况策略。  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>针对数据层应用程序的监视策略  
 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据层应用程序的使用过度和使用不足策略如下：  
  
-   数据层应用程序处理器使用率。  
  
-   用于数据库文件的数据层应用程序文件空间。  
  
-   用于存储卷的数据层应用程序文件空间。  
  
-   计算机处理器使用率。  
  
> [!NOTE]  
>  对于数据层应用程序，存储卷和处理器使用率为只读策略。  
  
 有关查看或更改数据层应用程序的全局监视策略的详细信息，请参阅[实用工具管理（SQL Server 实用工具）](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)。  
  
 有关查看或更改单独数据层应用程序的监视策略的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>针对 SQL Server 的托管实例的监视策略  
 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的使用过度和使用不足策略如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例处理器使用率。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例文件空间。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例文件空间。  
  
-   计算机处理器使用率。  
  
 有关查看或更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的全局监视策略的详细信息，请参阅[实用工具管理（SQL Server 实用工具](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)）。  
  
 有关查看或更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的单独托管实例的全局监视策略的详细信息，请参阅[托管实例详细信息（SQL Server 实用工具）](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
