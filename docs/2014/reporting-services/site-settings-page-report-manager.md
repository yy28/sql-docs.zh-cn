---
title: 站点设置页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4d67a01c-eae4-49ba-a6e8-8e983c0248f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07fc0207020887d7e3ceb8716ee76c78a55d2bac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101121"
---
# <a name="site-settings-page-report-manager"></a>“站点设置”页（报表管理器）
  使用“站点设置”页可以更改应用程序标题，为报表历史记录限制和报表处理超时值设置服务器范围的默认值，管理系统级角色分配以及管理共享计划。 必须拥有“内容管理员”和“系统管理员”权限才能查看此页。  
  
> [!NOTE]  
>  并非在 SQL Server 的每个版本中均提供以下功能：报表历史记录、报表执行和共享计划。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-site-settings-page"></a>打开“站点设置”页  
  
1.  打开报表管理器。  
  
2.  单击页面顶部的 **“站点设置”** 。 这会打开该站点的“常规属性”页。  
  
     **注意：** 如果没有看到**站点设置**选项菜单中，您没有所需的权限，有关详细信息，请参阅的"站点设置"部分[为本地管理配置本机模式报表服务器&#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 指定用于此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 报表管理器实例的标题。 默认情况下，标题是"[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]"。  
  
 **选择报表历史记录的默认设置**  
 为要保留的报表历史副本数选择默认值。 此默认值为报表历史记录的相关限制提供了初始设置。 您可以在报表级别更改这些设置。 有关详细信息，请参阅[“快照选项”属性页（报表管理器）](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)。  
  
 如果以后限制报表历史记录，则在现有的报表历史记录超出您指定的限制时，报表服务器将减少现有的报表历史记录以符合新限制。 首先删除最旧的报表快照。 如果报表历史为空或者低于限制，则添加新的报表快照。 到达限制后，将在添加新的报表快照时删除时间最早的快照。  
  
 **报表执行超时**  
 指定在给定的秒数之后报表处理是否超时。  
  
 此值应用于报表服务器上的报表处理。 它不会影响为报表提供数据的数据库服务器上的数据处理。  
  
 报表处理计时器时钟在您选择报表时开始运行，而在报表打开时结束运行。 设置该值时，请指定足够的时间以完成数据处理和报表处理。  
  
 **自定义报表生成器启动 URL**  
 当报表服务器不使用默认报表生成器 URL 时，可指定自定义 URL。 此设置是可选的。 如果不指定值，将使用默认 URL，此时报表生成器将作为 ClickOnce 应用程序启动。 默认 URL 为下列值之一：  
  
 **本机模式报表服务器：** 在本机模式安装中，默认 URL 将采用格式为 http://\<*computername*> / reportserver/ReportBuilder/ReportBuilder_3_0_0_0.application。  
  
 SharePoint 集成模式下：默认 URL 将采用格式为 http://\<*SharePoint_site*> / _vti_bin/ReportBuilder/ReportBuilder_3_0_0_0.application。"  
  
 **Apply**  
 单击此选项可保存对报表服务器所做的更改。  
  
 **安全性**  
 单击此链接可打开“系统角色分配”页，在该页可以向预定义的系统角色分配用户和组帐户。  
  
 **计划**  
 单击此链接将打开“计划”页，在该页可以预定义供用户选择以用于其报表和订阅的共享计划。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [预定义角色](security/role-definitions-predefined-roles.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
