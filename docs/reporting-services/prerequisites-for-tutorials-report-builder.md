---
title: "教程 （报表生成器） 的先决条件 |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2c2056dccbb2d65e880928e4ec37a70080cfbf53
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="prerequisites-for-tutorials-report-builder"></a>教程先决条件（报表生成器）

若要完成报表生成器教程，你需要能够在报表服务器上或与报表服务器集成的 SharePoint 站点上查看和保存 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 分页报表。 对于数据，所有的教程使用文本的查询必须处理的 SQL Server 实例。  
  
如果您无权访问报表服务器或站点或数据源，则可以通过生成脱机报表来了解报表生成器。 请参阅[教程：脱机创建快速图表报表（报表生成器）](../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)。  

## <a name="requirements"></a>要求

若要完成“报表生成器”教程，您必须满足下列先决条件：  
  
-   对报表生成器的访问。 可以在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 报表服务器上或 SharePoint 集成模式下的 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 报表服务器上运行报表生成器。 在其他服务器上只有第一步不同，即如何打开报表生成器。  
  
    在报表服务器上，选择“新建” > “分页报表”。
  
    在 SharePoint 集成模式下的报表服务器上，在“文档”选项卡上选择“新建文档”，然后从下拉列表中，选择“报表生成器报表”。 例如，`http://<servername>/sites/mySite/reports`。 SharePoint 管理员必须为每个文档库启用“报表生成器报表”功能。  
  
-   指向 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 报表服务器或与 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 报表服务器集成的 SharePoint 站点的 URL。 您必须拥有保存和查看报表、共享数据源、共享数据集、报表部件和模型的权限。 默认情况下，报表服务器的 URL 是 `http://<servername>/reportserver`。 默认情况下，SharePoint 站点的 URL 是 `http://<sitename>` 或 `http://<server>/site`。  
  
-   SQL Server 实例和凭据不足以对任何数据库的只读访问权限的名称。 这些教程中的数据集查询使用文字数据，但必须由 SQL Server 的实例返回元数据所需的报表数据集处理每个查询。 例如，以下连接字符串仅指定一个服务器： `data source=<servername>`。 您必须对默认数据库具有读取权限，该权限是由授予您对服务器的访问权限的系统管理员分配给您的。 您还可以指定数据库，如以下连接字符串中所示： `data source=<servername>;initial catalog=<database>`。  
  
-   有关[教程： 地图报表 （报表生成器）](Tutorial:%20Map%20Report%20\(Report%20Builder\).md)，必须将报表服务器配置为支持 Bing 地图作为背景。 有关详细信息，请参阅[计划地图报表支持](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19)。   

-   [教程： 创建钻取和 Main 报表 （报表生成器）](Tutorial:%20Creating%20Drillthrough%20and%20Main%20Reports%20\(Report%20Builder\).md)教程需要访问 Contoso Sales 多维数据集。 有关详细信息，请参阅该教程。 
  
报表服务器管理员必须向你授予对报表服务器的必要权限，配置 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 文件夹位置，并且配置报表生成器默认选项。 有关详细信息，请参阅 [安装和卸载报表生成器](http://msdn.microsoft.com/library/2c9a5814-17bf-4947-8fb3-6269e7caa416)。  

## <a name="next-steps"></a>后续步骤

[报表生成器教程](../reporting-services/report-builder-tutorials.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)

