---
title: PowerPivot 可用性和灾难恢复 (SQL Server 2014) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7c05bb8ca3e917d12fe1452dd598c30c698d3c4a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028245"
---
# <a name="powerpivot-availability-and-disaster-recovery-sql-server-2014"></a>PowerPivot 可用性和灾难恢复 (SQL Server 2014)
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的可用性和灾难恢复计划主要依赖于 SharePoint 场的设计、不同的组件可接受的停机时间量以及针对 SharePoint 可用性实现的工具和最佳实践。 本主题汇总了各种技术，并包含在为 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 部署计划可用性和灾难恢复时要考虑的示例拓扑关系图。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **本主题内容：**  
  
-   [实现 PowerPivot 高可用性的示例 SharePoint 2013 拓扑](#bkmk_sharepoint2013)  
  
-   [实现 PowerPivot 高可用性的示例 SharePoint 2010 拓扑](#bkmk_sharepoint2010)  
  
-   [PowerPivot 服务应用程序数据库以及 SQL Server 可用性和恢复技术](#bkmk_sql_server_technologies)  
  
-   [详细信息链接](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013"></a> 实现 PowerPivot 高可用性的示例 SharePoint 2013 拓扑  
 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署中，设计 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 可用性的方式更为灵活。 在 SharePoint 2013 中，在 SharePoint 模式中部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例（也称为 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务器）在 SharePoint 场的外部运行，并且可以安装到单独的服务器上。 SharePoint 模式中的每个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例都注册到 Excel Services 中。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共享服务和服务应用程序在 SharePoint 应用程序服务器上运行。  
  
 以下关系图说明了示例 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 部署。 此示例支持 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务的高可用性并假定数据库将定期备份。  
  
 ![在 2013年的 powerpivot 可用性](../media/ssas-powerpivot-services-2013.png "2013年中的 powerpivot 可用性")  
  
-   **(1)** Web 前端服务器。 使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 外接程序在每台服务器上安装数据提供程序。 有关详细信息，请参阅[安装或卸载 PowerPivot for SharePoint 外接程序&#40;SharePoint 2013&#41;](../instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)。  
  
-   **(2)** [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 共享服务在**每台**应用程序服务器上运行，并允许服务应用程序**跨多台**应用程序服务器运行。 因此，如果单一应用程序服务器处于脱机状态，则 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 应用程序仍将可用。  
  
-   **(3)** Excel Calculation Services 在每台应用程序服务器上运行，并允许服务应用程序跨多台应用程序服务器运行。 因此，如果单一应用程序服务器处于脱机状态改，则 Excel Calculation Services 仍将可用。  
  
-   **(4)** 和 **(6)** 的实例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]单元在 SharePoint 场外部的服务器上的 SharePoint 模式下运行，这包括 Windows 服务**SQL Server Analysis Services (POWERPIVOT)**。 所有这些实例都注册到 Excel Services 中 **(3)**。 Excel Services 管理向 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务器请求的负载平衡。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 体系结构使您能够拥有多台 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务器，以便能根据需要轻松添加多个实例。 有关详细信息，请参阅 [管理 Excel Services 数据模型设置 (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\).aspx)。  
  
-   **(5)** 用于内容、配置和应用程序数据库的 SQL Server 数据库。 这包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库。 您的 DR 计划应包括数据库层。 在此设计中，数据库在 **(4)** 某个 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 实例所在的服务器上运行。 **(4)** 和 **(5)** 还可以位于不同的服务器上。  
  
-   **(7)** 某种形式的 SQL Server 数据库备份或冗余。  
  
##  <a name="bkmk_sharepoint2010"></a> 实现 PowerPivot 高可用性的示例 SharePoint 2010 拓扑  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 体系结构要求所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 组件都在相同的 SharePoint 应用程序服务器上运行。 这包括 SharePoint 模式中部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例以及仅与 SharePoint 2013 部署中的某个实例比较的两个共享服务。  
  
 以下关系图说明了示例 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 部署。 此示例支持 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务的高可用性并假定数据库将定期备份。  
  
 ![在 sharepoint 2010 的 powerpivot 可用性](../media/ssas-powerpivot-services-2010.png "在 sharepoint 2010 的 powerpivot 可用性")  
  
-   **(1)** Web 前端服务器。 在每台服务器上安装数据访问接口。 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
-   **(2)** 两个[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]共享服务和 **(4)** Windows 服务**SQL Server Analysis Services (POWERPIVOT)** SharePoint 应用程序服务器上安装。  
  
     [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务  在每台应用程序服务器上运行，并允许服务应用程序跨多台  应用程序服务器运行。 如果单一应用程序服务器处于脱机状态，则 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务应用程序仍将可用。  
  
     若要增加 SharePoint 2010 中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 容量，请部署多个运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系统服务的 SharePoint 应用程序服务器。  
  
-   **(3)** Excel Calculation Services 在每台应用程序服务器上运行，并允许服务应用程序跨多台应用程序服务器运行。 因此，如果单一应用程序服务器处于脱机状态改，则 Excel Calculation Services 仍将可用。  
  
-   **(5)** 用于内容、配置和应用程序数据库的 SQL Server 数据库。 这包括 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序数据库。 您的 DR 计划应包括数据库层。  
  
-   **(6)** 某种形式的 SQL Server 数据库备份或冗余。  
  
##  <a name="bkmk_sql_server_technologies"></a> PowerPivot 服务应用程序数据库以及 SQL Server 可用性和恢复技术  
 包括 SharePoint 高可用性规划中的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 服务应用程序数据库。 此数据库的默认名称是 `DefaultPowerPivotServiceApplicationDB-<GUID>`。 下面总结了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用性技术以及与 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 数据库结合使用时的一些建议。 有关详细信息，请参阅 [SharePoint 数据库支持的高可用性和灾难恢复选项 (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)。  
  
||注释|  
|-|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 同步镜像以实现可用性。|支持，但不建议这样做。 建议使用同步 – 提交模式下的 AlwaysOn。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 同步 – 提交模式下|支持，建议这样做。|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 异步镜像或将日志传送到另一个服务器场以实现灾难恢复。|支持。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 使用异步提交以实现灾难恢复|是否支持|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志传送  
  
 有关如何使用 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]计划冷备用方案的详细信息，请参阅 [PowerPivot 灾难恢复](http://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx)。  
  
## <a name="verification"></a>验证  
 指南和脚本，帮助您验证[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]部署之前和之后的灾难恢复周期，请参阅[清单： 使用 PowerShell 验证 PowerPivot for SharePoint](../instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)。  
  
##  <a name="bkmk_more_resources"></a> 详细信息链接  
  
-   [SharePoint 数据库支持的高可用性和灾难恢复选项 (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)  
  
-   [规划灾难恢复 (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  
-   [SQL Server 云备份和恢复白皮书](http://www.microsoft.com/server-cloud/solutions/cloud-backup-recovery.aspx?WT.srch=1&WT.mc_ID=SEM_BING_USEvergreenSearch_Unassigned&CR_CC=Unassigned#fbid=RjU2Nbzu2dT)  
  
-   [Microsoft® SQL Server Backup to Microsoft Windows® Azure®Tool](http://www.microsoft.com/download/details.aspx?id=40740)  
  
 **社区内容**  
  
-   [在 SharePoint 2013 上管理服务实例](http://www.petri.co.il/manage-service-instances-sharepoint-2013.htm)  
  
-   [备份数据库 SQL Server 脚本](http://megaupl0ad.net/free/backup%20database%20sql%20server%20script)  
  
  