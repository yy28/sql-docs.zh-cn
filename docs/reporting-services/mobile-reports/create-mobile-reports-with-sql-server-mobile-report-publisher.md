---
title: "使用 SQL Server Mobile Report Publisher 创建移动报表 |Microsoft 文档"
description: "了解有关 Reporting Services 移动报表连接到本地数据，具有多种类型的数据可视化效果的移动设备。"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: a5a8dbf6-4c3a-435d-8188-d6656c32f229
caps.latest.revision: 35
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4fe797ac21e1f659b1a2a196be3f860a65b36896
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="create-mobile-reports-with-sql-server-mobile-report-publisher"></a>使用 SQL Server 移动报表发布服务器创建移动报表
了解 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 移动报表，其针对移动设备进行了优化，可连接到本地数据，且具有多种类型的数据可视化效果。 

>[!NOTE]
>  你是否需要将仪表板等 Kpi Datazen 服务器内容迁移到 SQL Server 2016[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]服务器？ 请尝试 [Datazen 的 SQL Server 迁移助手](https://www.microsoft.com/en-us/download/details.aspx?id=53128)。 
 
![SS_MRP_LayoutTabSm](../../reporting-services/media/ss-mrp-layouttabsm.png)  

通过 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]，可以快速创建 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 移动报表，它针对移动设备及其他外形规格进行了优化。 移动报表提供各式各样的可视化效果：从时间、类别和比较图表，到树状地图和自定义地图。 

* 将你的移动报表连接到各种数据源，包括本地 SQL Server 和 Analysis Services 数据。 
* 在网格行和列可调整且移动报表元素灵活的设计图面上设计移动报表，这些报表可轻松缩放至任何屏幕大小。 
* 然后将这些移动报表保存到 Reporting Services 服务器，并查看和浏览器中或在 Ipad、 Iphone、 Android 手机和平板电脑和 Windows 10 设备上的 Power BI 移动应用中与它们进行交互。
  
## <a name="create-includessrsnoversionmdincludesssrsnoversion-mdmd--mobile-reports"></a>创建 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  移动报表  
  
这些文章可帮助你入门。
-  下载 [SQL Server 移动报表发布服务器](http://go.microsoft.com/fwlink/?LinkID=733527)  
-  [创建 Reporting Services 移动报表](../../reporting-services/mobile-reports/create-a-reporting-services-mobile-report.md)  
-  [End-to-end walkthrough: Create mobile reports and KPIs in SQL Server 2016 Reporting Services（端到端演练：在 SQL Server 2016 Reporting Services 中创建移动报表和 KPI）](http://christopherfinlan.com/2015/12/21/how-to-create-mobile-reports-and-kpis-in-sql-server-reporting-services-2016-an-end-to-end-walkthrough/) （Christopher Finlan 博客）  
- [设计为先还是数据为先](../../reporting-services/mobile-reports/design-first-or-data-first-when-creating-in-reporting-services-mobile-reports.md)：决定是先使用模拟数据设计报表，还是使用自己的数据开始。  
- [用于 Reporting Services 移动报表的数据](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)：使用来自共享数据集的数据，或从 Excel 工作簿准备数据，以在移动报表中使用。
- [Reporting Services 中移动报表和 KPI 的数据刷新工作原理](http://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/) （Christopher Finlan 的博客）：了解如何设置共享数据集的缓存，以便控制刷新数据的频率并提升报表性能。
- [移动报表中的可视化效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
- [移动报表中的仪表](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
- [移动报表中的地图](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
- 利用颜色和企业标志[设置 Web 门户和移动报表的外观](../../reporting-services/branding-the-web-portal.md) 
  
## <a name="ssrs-mobile-reports-in-the-power-bi-mobile-apps"></a>Power BI 移动应用中的 SSRS 移动报表

-  视图[Reporting Services 移动报表和 Kpi 的 iOS 移动应用中](https://powerbi.microsoft.com/documentation/powerbi-mobile-iphone-kpis-mobile-reports)
-  视图[Reporting Services 移动报表和 Android 设备的 Power BI 应用中的 Kpi](https://powerbi.microsoft.com/documentation/powerbi-mobile-android-kpis-mobile-reports)
-  [Windows 10 设备 Power BI 应用中的 Reporting Services 移动报表和 KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/)    

## <a name="see-also"></a>另请参阅  
  
-   [创建、修改和删除共享数据源 (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
-   [管理共享数据集](../../reporting-services/report-data/manage-shared-datasets.md)  
-  [使用 Reporting Services 中的 KPI](../../reporting-services/working-with-kpis-in-reporting-services.md)  
- [启用报表服务器以允许进行 Power BI 移动访问](../../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)  

  
  


