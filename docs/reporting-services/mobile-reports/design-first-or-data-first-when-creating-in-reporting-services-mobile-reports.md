---
title: 创建 Reporting Services 移动报表时先从设计或数据开始 | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cf9afd8c4aa916d87929a8e7d73347cc33456252
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63066629"
---
# <a name="design-first-or-data-first-when-creating-in-reporting-services-mobile-reports"></a>Design first or data first when creating in Reporting Services mobile reports
  
借助 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]，可以在网格行和列可调整且移动报表元素灵活的设计图面上快速创建移动报表，这些报表可轻松缩放至任何屏幕大小。   
  
创建移动报表时，有两种基本方法供你选择：先从数据开始或先从设计开始。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 对这两种方法都支持。   
  
## <a name="design-first"></a>设计为先  
  
下图显示了 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 布局视图的组件：   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
在设计为先的方法中，首先创建移动报表布局，无需导入任何数据。 如果你不能确定数据的格式是否正确，这是一个创建移动报表的好办法。 如果没有实际数据，库元素自动绑定到生成的模拟数据，你可以将数据导出并用作为模板来描述所需的数据。  
  
## <a name="data-first"></a>数据为先  
数据为先的方法是先导入所有必需的数据，设计移动报表，然后在移动报表元素中设置数据属性。 这种方法具有一个优势，即当你将每个元素添加到布局中时能够将其与实际数据相连。 使用数据为先的方法时，请确保实际数据的格式正确无误，可用于 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]。   
  
 下图显示了 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 数据视图的所有组件：  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### <a name="see-also"></a>另请参阅  
- [使用 SQL Server Mobile Report Publisher 创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [在 iPad 应用中查看 SQL Server 移动报表和 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI for iOS)  
-  [View SQL Server mobile reports and KPIs in the iPhone app (Power BI for iOS)（在 iPhone 应用 (Power BI for iOS) 中查看 SQL Server 移动报表和 KPI）](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports)  
  
  
  
  

