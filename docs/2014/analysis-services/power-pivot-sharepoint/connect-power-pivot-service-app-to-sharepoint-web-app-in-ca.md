---
title: 将 PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da816635ab978e7baadfb810aed78fa0f3258dd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071681"
---
# <a name="connect-a-powerpivot-service-application-to-a-sharepoint-web-application-in-central-administration"></a>将 PowerPivot 服务应用程序连接到管理中心中的 SharePoint Web 应用程序
  PowerPivot 服务应用程序可由场中任意数目的 SharePoint Web 应用程序使用。 若要使 PowerPivot 服务应用程序可用，请将其添加到服务关联列表中。  
  
> [!IMPORTANT]  
>  默认组中必须有一个 PowerPivot 服务应用程序，以确保 PowerPivot 管理面板正确工作。 不要向默认组添加多个 PowerPivot 服务应用程序。 添加同一服务应用程序类型的多个条目是不支持的配置并且可能导致错误。 如果您要创建其他服务应用程序，请将它们添加到自定义列表。  
  
 本主题包含以下各节：  
  
 [将 PowerPivot 服务应用程序添加到默认组](#default)  
  
 [将 PowerPivot 服务应用程序添加到自定义服务关联列表](#custom)  
  
##  <a name="add-powerpivot-services-application-to-the-default-group"></a><a name="default"></a>将 PowerPivot 服务应用程序添加到默认组  
 服务关联列表是向场中的其他 SharePoint Web 应用程序提供资源的共享服务的列表。 场有一个默认的服务关联组。  
  
 若要将 PowerPivot 服务应用程序添加到该列表中，您既可以在创建应用程序时添加，也可以在之后采用以下步骤添加。  
  
1.  在“管理中心”的 **“应用程序管理”** 中，单击 **“配置服务应用程序关联”**。  
  
2.  在“应用程序代理组”中，单击 **“默认值”**。  
  
3.  选中 PowerPivot 服务应用程序旁边的复选框（由类型名称 `PowerPivot Service Application Proxy` 指示）。 如果有多个 PowerPivot 服务应用程序，请只选择一个。  
  
4.  单击" **确定**"。  
  
##  <a name="add-powerpivot-services-application-a-custom-service-association-list"></a><a name="custom"></a>添加 PowerPivot 服务应用程序自定义服务关联列表  
 默认组可由自定义列表替换。 自定义列表是专门为单个 SharePoint Web 应用程序创建的。 它覆盖默认组，并且仅使用场管理员或服务管理员指定的服务关联来替换它。 如果您创建了多个 PowerPivot 服务应用程序，则必须使用自定义列表指定要使用的应用程序。 自定义列表不能由其他 Web 应用程序重用。 它仅适用于为其创建的 Web 应用程序。  
  
1.  在“管理中心”的 **“应用程序管理”** 中，单击 **“管理 Web 应用程序”**。  
  
2.  选择应用程序（例如 SharePoint -80）。  
  
3.  在“Web 应用程序”的“管理”中，单击 **“服务连接”**。  
  
4.  在“编辑以下连接组”**** 中，选择“[custom]”****。  
  
5.  选中您要使用的每个服务应用程序连接旁边的复选框。 如果您有多个 PowerPivot 服务应用程序（由设置为 `PowerPivot Service Application Proxy` 的类型指示），请确保仅选择一个。  
  
6.  单击" **确定**"。  
  
## <a name="see-also"></a>另请参阅  
 [在管理中心中创建和配置 PowerPivot 服务应用程序](create-and-configure-power-pivot-service-application-in-ca.md)   
 [初始配置 &#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)  
  
  
