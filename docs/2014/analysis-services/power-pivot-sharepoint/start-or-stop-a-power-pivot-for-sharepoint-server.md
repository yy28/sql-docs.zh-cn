---
title: 启动或停止 PowerPivot for SharePoint Server |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df2305d3efa7896d8646be33a5f95ade8c4e7c00
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247387"
---
# <a name="start-or-stop-a-powerpivot-for-sharepoint-server"></a>启动或停止 PowerPivot for SharePoint 服务器
  PowerPivot 系统服务和一个[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]实例相同的本地应用程序服务器，以支持 SharePoint 场内协调一致的请求和数据处理上一起运行。  
  
 本主题包含以下各节：  
  
 [服务依赖关系](#dependencies)  
  
 [启动或停止服务](#startstop)  
  
 [停止 PowerPivot 服务器的影响](#effects)  
  
##  <a name="dependencies"></a> 服务依赖关系  
 PowerPivot 系统服务依赖本地 Analysis Services 服务器实例，它们一起安装在同一物理服务器上。 如果停止 PowerPivot 系统服务，也必须手动停止本地 Analysis Services 服务器实例。 如果一个服务正在运行而其他服务器实例未运行，则您将遇到针对 PowerPivot 数据处理的请求分配错误。  
  
 只有在您诊断或解决问题时，Analysis Services 服务器才应单独运行。 在所有其他情况下，该服务器都需要在同一服务器上本地运行的 PowerPivot 系统服务。  
  
##  <a name="startstop"></a> 启动或停止服务  
 始终使用管理中心来启动或停止 PowerPivot 系统服务或 Analysis Services 服务器实例。 通过管理中心，您可以从同一页一起启动或停止服务。 此外，管理中心使用称作 **“一个或多个服务已启动或停止”** 的计时器作业来重新启动它认为应运行的服务。 如果您使用非 SharePoint 工具停止 PowerPivot 系统服务或 Analysis Services，则在该计时器作业运行时这些服务将重新启动。  
  
 启动和停止服务是一种应用于物理服务实例的操作。 如果场中还有其他 PowerPivot for SharePoint 服务器，场中的其他服务器将继续接受对 PowerPivot 数据的请求。  
  
 不能同时启动或停止场内的所有物理服务。 必须选择每个服务器，然后启动或停止特定服务。  
  
 不能启动、暂停或停止特定 Web 应用程序的 PowerPivot 系统服务，但可以从默认连接列表中删除服务，使其不可用。 有关详细信息，请参阅[PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)。  
  
1.  在管理中心的 **“系统设置”** 中，单击 **“管理服务器上的服务”**。  
  
2.  在本页顶部的“服务器”中，单击下箭头，然后单击 **“更改服务器”**。  
  
3.  选择具有您要启动或停止的 PowerPivot 系统服务或 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]实例的 SharePoint 服务器。  
  
4.  选择服务，然后单击该操作。 记住要成对启动或停止服务。 如果您启动或停止 PowerPivot 系统服务，请务必还要启动或停止在同一台计算机上运行的 Analysis Services 服务器实例。  
  
##  <a name="effects"></a> 停止 PowerPivot 服务器的影响  
 下表介绍了在 SharePoint 服务器上停止 PowerPivot 系统服务和 Analysis Services 服务的影响。  
  
|影响的对象|Description|  
|---------------|-----------------|  
|现有查询|Analysis Services 服务器上正在进行中的查询将立即停止。 用户将收到“找不到数据”或“找不到数据源连接”错误。|  
|当前正在进行处理的现有数据刷新作业|当前 Analysis Services 服务器上正在进行中的作业将立即停止。 数据刷新操作将失败，而且将在数据刷新历史记录中记录一个错误。<br /><br /> 在停止服务之前，您可以使用 SharePoint 管理中心的”检查作业状态“页查看当前作业的状态。<br /><br /> 尽管可以知道哪些作业当前正在处理，但没有办法通过查看队列本身来了解是否有其他作业将要启动。|  
|队列中的现有数据刷新请求|在计划的整个执行过程中，计划的数据刷新请求将一直保留在处理队列中（也就是说，计划的数据刷新请求将一直保持在队列中，直到下一次启动）。 如果到那时 PowerPivot 系统服务没有重新启动，数据刷新请求将被删除，并且将记录一个错误。|  
|新的查询或数据刷新请求|如果您要停止场中的唯一一个 PowerPivot for SharePoint 服务器，新的 PowerPivot 数据请求将不被处理，而且数据请求将导致“找不到数据”错误。<br /><br /> 如果有其他 PowerPivot for SharePoint 服务器，请求将转到其中的一个可用服务器。|  
|使用情况数据|服务停止时将不会收集使用情况数据。|  
  
## <a name="see-also"></a>请参阅  
 [配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)  
  
  
