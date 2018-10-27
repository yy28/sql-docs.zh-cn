---
title: Power Pivot 服务应用连接到 CA 中的 SharePoint Web 应用 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd72f62cc513064e01c04e5a501b18a070f4c7a8
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50098970"
---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Power Pivot 服务应用连接到 CA 中的 SharePoint Web 应用
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序可由场中任意数目的 SharePoint Web 应用程序使用。 若要使 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序可用，请将其添加到服务关联列表中。  
  
> [!IMPORTANT]  
>  默认组中必须有一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，以确保 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板正常工作。 不要向默认组添加多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序。 添加同一服务应用程序类型的多个条目是不支持的配置并且可能导致错误。 如果您要创建其他服务应用程序，请将它们添加到自定义列表。  
  
 本主题包含以下各节：  
  
 [将 Power Pivot 服务应用程序添加到默认组](#default)  
  
 [将 Power Pivot 服务应用程序添加到自定义服务关联列表](#custom)  
  
##  <a name="default"></a> 将服务应用程序添加到默认组  
 服务关联列表是向场中的其他 SharePoint Web 应用程序提供资源的共享服务的列表。 场有一个默认的服务关联组。  
  
 若要将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序添加到该列表中，你既可以在创建应用程序时添加，也可以在之后采用以下步骤添加。  
  
1.  在“管理中心”的 **“应用程序管理”** 中，单击 **“配置服务应用程序关联”**。  
  
2.  在“应用程序代理组”中，单击 **“默认值”**。  
  
3.  选中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序（表示为类型名称“PowerPivot 服务应用程序代理”）旁边的复选框。 如果有多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，请只选择一个。  
  
4.  单击“确定” 。  
  
##  <a name="custom"></a> 将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序添加到自定义服务关联列表  
 默认组可由自定义列表替换。 自定义列表是专门为单个 SharePoint Web 应用程序创建的。 它覆盖默认组，并且仅使用场管理员或服务管理员指定的服务关联来替换它。 如果你创建了多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序，则必须使用自定义列表指定要使用的应用程序。 自定义列表不能由其他 Web 应用程序重用。 它仅适用于为其创建的 Web 应用程序。  
  
1.  在“管理中心”的 **“应用程序管理”** 中，单击 **“管理 Web 应用程序”**。  
  
2.  选择应用程序（例如 SharePoint -80）。  
  
3.  在“Web 应用程序”的“管理”中，单击 **“服务连接”**。  
  
4.  在“编辑以下连接组”中，选择“[custom]”。  
  
5.  选中您要使用的每个服务应用程序连接旁边的复选框。 如果有多个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序（表示为“PowerPivot 服务应用程序代理”的类型集），请确保仅选择一个。  
  
6.  单击“确定” 。  
  
## <a name="see-also"></a>另请参阅  
 [在管理中心中创建和配置 Power Pivot 服务应用程序](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [初始安装 (Power Pivot for SharePoint)](http://msdn.microsoft.com/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
