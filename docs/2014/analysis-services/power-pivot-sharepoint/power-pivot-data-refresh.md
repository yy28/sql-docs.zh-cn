---
title: PowerPivot 数据刷新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6f7d5ed5c2f8882cbc0c47a1c711748d26e0193c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535069"
---
# <a name="powerpivot-data-refresh"></a>PowerPivot 数据刷新
  在您创建包含 PowerPivot 数据的某一工作簿后，最好通过重新运行查询或命令以便从您最初用于创建该工作簿的数据源获取更新的信息，定期刷新数据。 此过程称作 `data refresh`，并且您可以在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 中按需刷新数据，或者作为在 SharePoint 场中的应用程序服务器上以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进程形式运行的定期操作来刷新数据。 有关详细信息，请参见:  
  
-   [使用 SharePoint 2010 进行 PowerPivot 数据刷新](../powerpivot-data-refresh-with-sharepoint-2010.md)  
  
-   [将 PowerPivot 无人参与的数据刷新帐户配置 &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
-   [为 PowerPivot 数据刷新配置存储的凭据 &#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
-   [计划数据刷新 &#40;PowerPivot for SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
-   [查看数据刷新历史记录 &#40;PowerPivot for SharePoint&#41;](view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SharePoint Server 2013 Excel Services 使用不同的体系结构对 PowerPivot 数据模型进行数据刷新。 SharePoint 2013 支持的体系结构利用 Excel Services 作为主要组件加载 PowerPivot 数据模型。 以前的数据刷新体系结构依赖在 SharePoint 模式下运行 PowerPivot 系统服务和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的服务器来加载数据模型。 有关详细信息，请参阅以下部分：  
> 
>  -   [使用 SharePoint 2013 进行 PowerPivot 数据刷新](power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [&#40;SharePoint 2013&#41;升级工作簿和计划的数据刷新](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
