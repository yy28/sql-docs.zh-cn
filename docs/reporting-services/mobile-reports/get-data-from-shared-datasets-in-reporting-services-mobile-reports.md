---
title: "从 Reporting Services 移动报表中的共享数据集获取数据 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b846451-c8d0-412c-802d-a42bb1ff8c63
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c081588c29dddd792d0b92e6cd9573beeb09fa4f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="get-data-from-shared-datasets-in-reporting-services-mobile-reports"></a>Get data from shared datasets in Reporting Services mobile reports
除了[从 Excel 文件加载数据](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)，SQL Server 移动报表发布服务器还可以从几乎任何源访问数据。 访问数据需要配置 Reporting Services web 门户上的共享的数据源。 了解有关 [创建共享数据源](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 和 [创建共享数据集](../../reporting-services/report-data/manage-shared-datasets.md)的详细信息。  
  
共享数据源以及共享数据集配置 Reporting Services 服务器上后，可以在创建的移动报表中使用它们[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。   
  
从 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 连接到 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]服务器后，将移动报表连接到共享数据集非常简单。   
  
1. 在 **数据** 选项卡上，选择 **添加数据**。  
  
2. 选择 **报表服务器**。   
  
3.  如果这是首次连接到服务器，请填写服务器名称以及你的用户名和密码。 将服务器名称按以下格式放入服务器地址框：  
  
    \<"servername"> /reports/  
  
    在此示例中:  
       
    ![SSMRP_ConnectToServer](../../reporting-services/mobile-reports/media/ssmrp-connecttoserver.png)  
      
  
4. 选择 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 服务器时，会看到文件夹中的可用数据集。 选择数据集将数据导入 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]。  
  
   ![SS_MRP_ServerData](../../reporting-services/mobile-reports/media/ss-mrp-serverdata.png)  
  
导入数据集后，可以按照自己的意愿使用模拟数据或 Excel 文件中的本地数据设计移动报表。  
  
默认情况下，共享数据集始终确保是最新数据，因为每次用户查看基于该数据集的移动报表时，SQL Server 都会运行基础查询并返回最新数据。 显然，如果很多人查看你的移动报表，这个方法可能并不适合，因此你可以设置缓存，以定期运行查询并缓存生成的数据集。 此博客文章介绍 [Web 门户中缓存和数据刷新的工作原理](http://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/)。  
  
## <a name="add-edit-or-remove-a-report-server"></a>添加、编辑或删除报表服务器  
  
如果已连接到报表服务器，在“数据”选项卡上选择“添加数据”后，将看不到用于添加另一个报表服务器的选项。 这时应执行以下步骤：  
  
1. 选择左上角的“连接”。  
  
   ![SSMRP_AddConnectionIcon](../../reporting-services/mobile-reports/media/ssmrp-addconnectionicon.png)  
     
   “服务器连接”窗格在右侧打开。  
     
   ![SSMRP_ServerConnectnPane](../../reporting-services/mobile-reports/media/ssmrp-serverconnectnpane.png)  
     
2. 添加新的服务器连接，或者编辑或删除现有的连接。  
  
### <a name="see-also"></a>另请参阅  
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [Web 门户 （SSRS 本机模式）](../../reporting-services/web-portal-ssrs-native-mode.md)  
-  [在 iPad 应用中查看 SQL Server 移动报表和 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  [View SQL Server mobile reports and KPIs in the iPhone app (Power BI for iOS)（在 iPhone 应用 (Power BI for iOS) 中查看 SQL Server 移动报表和 KPI）](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  


