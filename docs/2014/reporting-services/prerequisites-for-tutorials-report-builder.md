---
title: 教程先决条件（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9b8346a6-f4f4-4ad3-bc98-8f2be342ef2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 17c8b67d29cb82956a37bc3f83867161486a4f9e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73637868"
---
# <a name="prerequisites-for-tutorials-report-builder"></a>教程先决条件（报表生成器）
  “报表生成器”教程是希望您能够在报表服务器上或与报表服务器集成的 SharePoint 站点上查看和保存报表。 对于数据，所有教程都使用必须由 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 实例处理的文字查询。  
  
 如果您无权访问报表服务器或站点或数据源，则可以通过生成脱机报表来了解报表生成器。 请参阅[教程：脱机创建快速图表报表（报表生成器）](report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)。  
  
## <a name="requirements"></a>要求  
 若要完成“报表生成器”教程，您必须满足下列先决条件：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]对报表生成器的访问权限。 可以使用报表生成器的独立版本或 ClickOnce 版本（可从报表管理器或 SharePoint 站点获取），来运行报表生成器。 ClickOnce 版本只有第一步（如何打开报表生成器）不同。  
  
     若要使用报表管理器，请打开报表管理器并单击 "**报表生成器**"。 默认情况下，报表管理器的 URL 为 http://\<*servername*>/reports。  
  
     若要使用 SharePoint 站点，请导航至该站点，单击“文档”选项卡，再单击“新建文档”，然后从下拉列表中单击“报表生成器报表”。 例如，http://\<servername>/sites/mysite/reports。 SharePoint 管理员必须为每个文档库启用“报表生成器报表”功能。  
  
-   指向 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 报表服务器或与 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 报表服务器集成的 SharePoint 站点的 URL。 您必须拥有保存和查看报表、共享数据源、共享数据集、报表部件和模型的权限。 默认情况下，Report Server 的 URL 为 http://\<servername>/reportserver。 默认情况下，SharePoint 站点的 URL 是 http://\<sitename> 或 http://\<server>/site。  
  
-   
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 实例的名称和足以对任何数据库进行只读访问的凭据。 各教程中的数据集查询使用文字数据，但必须由 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 实例处理每个查询以返回报表数据集所必需的元数据。 例如，以下连接字符串仅指定一个服务器： `data source=<servername>`。 您必须对默认数据库具有读取权限，该权限是由授予您对服务器的访问权限的系统管理员分配给您的。 您还可以指定数据库，如以下连接字符串中所示： `data source=<servername>;initial catalog=<database>`。  
  
-   对于包括地图的教程，报表服务器必须配置为支持将 Bing 地图作为背景。 有关详细信息，请参阅 msdn.microsoft.com 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)的[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]文档中[的规划地图报表支持](plan-for-map-report-support.md)。  
  
-   教程[：创建钻取报表和主报表 &#40;报表生成器&#41;](tutorial-creating-drillthrough-and-main-reports-report-builder.md)，使用 Contoso 商业智能演示数据集。 此数据集由 ContosoDW 数据仓库和 Contoso_Retail 联机分析处理 (OLAP) 数据库组成。 您将在此教程中创建的报表从 Contoso Sales 多维数据集检索报表数据。 Contoso_Retail OLAP 数据库可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=18279)下载。 您只需要下载文件 ContosoBIdemoABF.exe。 它包含 OLAP 数据库。  
  
     另一个文件 ContosoBIdemoBAK.exe 用于 ContosoDW 数据仓库，在此教程中不使用它。  
  
     网站包含将 ContosoRetail.abf 备份文件提取和还原到 Contoso_Retail OLAP 数据库的说明。  
  
     您必须具有访问安装 OLAP 数据库的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的权限。  
  
 报表服务器管理员必须向你授予对报表服务器的必要权限，配置 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 文件夹位置，并且配置报表生成器默认选项。 有关详细信息，请参阅[安装、卸载和报表生成器支持](install-uninstall-and-report-builder-support.md)。  
  
## <a name="see-also"></a>另请参阅  
 [教程 &#40;报表生成器&#41;](report-builder-tutorials.md)  
  
  
