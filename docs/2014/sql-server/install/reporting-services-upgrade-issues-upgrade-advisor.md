---
title: Reporting Services 升级问题（升级顾问） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e2f39ea7b911f2ca83767dcfbfd82947acd4f52
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059011"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Reporting Services 升级问题（升级顾问）
  以下主题介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可能会影响升级到的问题 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。 这些主题介绍你可以采取哪些措施来缓解这些更改对环境的影响。  
  
 升级顾问可分析报表服务器安装。 如果仅安装了客户端组件（例如，如果报表设计器是安装在计算机中的唯一 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件），则不会报告任何问题。  
  
 根据安装的配置方式，您可能会遇到升级顾问未报告的其他问题。 这些问题不会阻止 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 升级成功，但是它们可能影响升级完成后报表和应用程序的运行方式。 若要了解这些问题，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“Reporting Services 的向后兼容性”。  
  
 如果无法使用安装程序升级 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装，你可以安装新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例并将现有安装迁移到新的实例。 有关详细信息，请参阅联机丛书中的 "升级和迁移 Reporting Services" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，[然后 Reporting Services 升级和迁移](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
 以下主题介绍升级顾问报告的已知问题，并解释可以如何修改现有安装以顺利进行升级。  
  
> [!IMPORTANT]  
>  若要分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例，升级顾问必须安装在报表服务器上。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不支持远程分析。  
>   
>  有关详细信息，请参阅[安装升级顾问](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [Report Server 网站上的客户端证书 &#40;升级顾问&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [在升级顾问 &#40;Report Server 上检测到自定义扩展&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [在升级顾问 &#40;Report Server 上检测到自定义报表项&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [&#40;升级顾问未检测到 IIS 向后兼容组件&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [&#40;升级顾问检测到 IP 地址限制&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [在 Report Server 站点 &#40;升级顾问上检测到 ISAPI 筛选器&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [在 Report Server 计算机 &#40;升级顾问上检测到过时的扩展&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [&#40;升级顾问&#41;未配置报表服务器数据库](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server 2005 &#40;升级顾问检测到报表服务器 Web 服务组&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [&#40;升级顾问指定虚拟目录&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [虚拟目录具有不受支持的身份验证方法 &#40;升级顾问&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [SQL Server Standard 和 Enterprise &#40;Upgrade Advisor 的 CPU 和内存限制的变化&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [SharePoint 场 &#40;升级顾问所需的域帐户&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [直接浏览到报表服务器 &#40;升级顾问&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 安装 &#40;升级顾问&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services SharePoint 共享服务是并行 &#40;升级顾问安装的&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [升级顾问 &#40;数据库引擎服务器排序规则不兼容&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [其他 Reporting Services 升级问题](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
