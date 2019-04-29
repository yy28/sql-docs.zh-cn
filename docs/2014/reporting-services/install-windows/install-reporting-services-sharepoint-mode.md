---
title: Reporting Services SharePoint 模式下安装 （SharePoint 2010 和 SharePoint 2013） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 656cf7489d4cc9d318a2ffce66bc1d0c8ff1d397
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63064644"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Reporting Services SharePoint 模式安装（SharePoint 2010 和 SharePoint 2013）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在 SharePoint 模式下是服务器组件，提供报表生成和传送，基于集合[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[msCoName](../../includes/msconame-md.md)]SharePoint 产品。  
  
 在 SharePoint 模式下运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 和数据警报功能。 有关 SharePoint 模式下的功能的详细信息，请参阅"支持和行为差异的服务器模式划分的功能"一节中[Reporting Services 报表服务器](../reporting-services-report-server.md)  
  
 对于 SharePoint 模式下的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，需要两个基本安装：  
  
|安装|Description|  
|------------------|-----------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用于 SharePoint 产品外接程序。|该外接程序在 SharePoint Web 前端服务器上安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用户界面 (UI) 页和功能。 UI 功能包括 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、SharePoint 管理中心中的管理页、在 SharePoint 文档库内使用的功能页以及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据警报页。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 模式下安装报表服务器|该报表服务器处理数据和报表处理和呈现以及订阅和数据警报处理。 SharePoint 模式报表服务器构建并安装为 SharePoint 共享服务。|  
  
 若要安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，请使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质。  
  
 有关高级的部署方案的说明，请参阅[部署核对清单：Reporting Services、 Power View 和 PowerPivot for SharePoint](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)和[部署核对清单：Reporting Services 安装到现有 SharePoint 场](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [支持的 SharePoint 和 Reporting Services 服务器及外接程序的组合&#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [安装适用于 SharePoint 2013 的 Reporting Services SharePoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [安装或卸载 Reporting Services 外接程序的 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [在何处查找用于 SharePoint 产品的 Reporting Services 外接程序](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [向场中添加另一个报表服务器（SSRS 扩展）](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [向场中添加另一个 Reporting Services Web 前端](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [用于 SSRS 服务应用程序的设置订阅和警报](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Claims to Windows Token Service &#40;C2WTS&#41;和 Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>请参阅  
 [数据警报体系结构和工作流](../reporting-services-data-alerts.md#AlertingWF)   
 [向管理员提出警报的数据警报管理器](../data-alert-manager-for-alerting-administrators.md)  
  
  
