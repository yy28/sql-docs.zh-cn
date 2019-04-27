---
title: Reporting Services 升级问题 （升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ed4ae6c15a16c3db009145f7daa995988ac04fbf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753679"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Reporting Services 升级问题（升级顾问）
  下面的主题介绍[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]可能会影响您升级到的问题[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 主题介绍可用于缓解对您的环境的这些更改影响的操作。  
  
 升级顾问可分析报表服务器安装。 如果仅安装了客户端组件（例如，如果报表设计器是安装在计算机中的唯一 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件），则不会报告任何问题。  
  
 根据安装的配置方式，您可能会遇到升级顾问未报告的其他问题。 这些问题不会阻止 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级成功，但是它们可能影响升级完成后报表和应用程序的运行方式。 若要了解这些问题，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“Reporting Services 的向后兼容性”。  
  
 如果您不能使用安装程序升级[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安装中，可以安装一个新[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实例，并将你的现有安装迁移到新实例。 详细信息，请参阅"升级和迁移 Reporting Services"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书[升级和迁移 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
 以下主题介绍升级顾问报告的已知问题，并解释可以如何修改现有安装以顺利进行升级。  
  
> [!IMPORTANT]  
>  若要分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，升级顾问必须安装在报表服务器上。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支持远程分析。  
>   
>  有关详细信息，请参阅[安装升级顾问](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [报表服务器网站上的客户端证书&#40;升级顾问&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [报表服务器上检测到自定义扩展插件&#40;升级顾问&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [报表服务器上检测到自定义报表项&#40;升级顾问&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [未检测到 IIS 向后兼容组件&#40;升级顾问&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [检测到的 IP 地址限制&#40;升级顾问&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [在报表服务器站点上检测到 ISAPI 筛选器&#40;升级顾问&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [报表服务器计算机上检测到过时的扩展插件&#40;升级顾问&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [未配置报表服务器数据库&#40;升级顾问&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [检测到的 SQL Server 2005 报表服务器 Web 服务组&#40;升级顾问&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [未指定虚拟目录&#40;升级顾问&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [虚拟目录具有不受支持的身份验证方法&#40;升级顾问&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [对 SQL Server Standard 和 Enterprise 的 CPU 和内存限制更改&#40;升级顾问&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [为 SharePoint 场要求使用域帐户&#40;升级顾问&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [直接浏览到报表服务器&#40;升级顾问&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [安装 Microsoft SharePoint 2007&#40;升级顾问&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services SharePoint 共享服务是并行安装&#40;升级顾问&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [不兼容的数据库引擎服务器排序规则&#40;升级顾问&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [其他 Reporting Services 升级问题](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
