---
title: 部署清单：Reporting Services 安装到现有 SharePoint 场 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 27e6b4a1fb9726496ac4ae99a08b2e47a9136562
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399660"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>部署清单：将 Reporting Services 安装到现有 SharePoint 场中
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 报表服务器可安装到新 SharePoint 场或现有 SharePoint 场。 本主题介绍将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装到现有 SharePoint 场的可能方案和最佳做法。  
  
## <a name="prerequisites"></a>先决条件  
 在运行安装程序之前，请查看以下信息：  
  
|步骤|链接|  
|----------|----------|  
|创建或标识报表服务器部署中使用的帐户。 必须具有报表服务器服务的服务帐户以及用来连接到报表服务器数据库的凭据||  
|确定用于承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地或远程实例。 您选择的实例所在计算机的存储容量应能够容纳报表。||  
|（可选）如果您要在订阅中使用报表服务器电子邮件，请查找为单位提供电子邮件服务的 SMTP 服务器或网关的名称|[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|注意：如果您要从早期 CTP 版本的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升级计算机并且您已对配置文件进行了自定义更改，则升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后您将需要对配置文件进行相同的更改。 受影响的文件**web.config**并**client.config**。||  
  
## <a name="installation-scenarios"></a>安装方案  
 下表介绍将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装到现有 SharePoint 场时的可能方案。 本地模式允许在本地从 SharePoint 文档库呈现报表，而无需与 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器集成。 用于 SharePoint 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序是必需的，但 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器不是。 有关本地模式的详细信息，请参阅[报表查看器中的本地模式和连接模式下的报表在报表查看器中&#40;SharePoint 模式下的 Reporting Services&#41; ](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)并[在哪里可以找到 Reporting Services 外接程序用于 SharePoint 产品](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
|启动配置|工作流|结束配置|注释|  
|----------------------------|--------------|--------------------------|--------------|  
|本地模式下的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|安装|连接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]连接模式 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 |就地升级|连接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]连接模式 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 |迁移|连接模式 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>安装和就地升级核对清单  
 下表汇总了您应该查看并用于安装的步骤、工具和信息：  
  
|步骤|链接|  
|----------|----------|  
|**安装和初始配置**||  
|在所有 Web 前端 (WFE) 计算机上安装 SharePoint 外接程序。|[向场中添加另一个 Reporting Services Web 前端](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|安装 SQL Server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services 和数据库引擎。|[安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少创建一个 SSRS 服务应用程序，并配置服务应用程序关联。|请参阅中的服务应用程序部分[安装 Reporting Services SharePoint 模式适用于 SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**其他配置**||  
|向文档库添加 SSRS 内容类型。|[将报表服务器内容类型添加到库&#40;Reporting Services SharePoint 集成模式下&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|设置 SQL Server 代理|[用于 SSRS 服务应用程序的设置订阅和警报](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|为您的服务应用程序配置电子邮件设置|[为 Reporting Services 服务应用程序配置电子邮件（SharePoint 2010 和 SharePoint 2013）](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|配置 Claims to Windows Token Service (c2WTS)|[Claims to Windows Token Service &#40;C2WTS&#41;和 Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>迁移核对清单  
 以下是从现有安装迁移到新安装的基本步骤的列表。  
  
|步骤|链接|  
|----------|----------|  
|安装并配置新服务器。 其中包括：<br /><br /> SharePoint 产品准备工具<br /><br /> SharePoint 2010 产品<br /><br /> SharePoint 2010 SP1<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 模式下的 <br /><br /> 用于 SharePoint 2010 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序|[安装用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|至少创建一个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序||  
|备份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据库||  
|备份 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 加密密钥||  
|还原 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 数据库和加密密钥||  
|将所有 Web 应用程序映射到新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服务应用程序| |  
|删除旧服务器上的集成 URL。|在 SharePoint 管理中心内的 **“常规应用程序设置”** 页上，单击 **“Reporting Services 集成”**。|  
|如果需要，从旧安装中卸载 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。||  
  
## <a name="next-steps"></a>后续步骤  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services SharePoint 模式下安装&#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [在 SharePoint 2010 场中使用 SQL Server BI 功能指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [支持的 SharePoint 和 Reporting Services 服务器及外接程序的组合&#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
