---
title: "添加到移动报表的数据网格 |Reporting Services |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
caps.latest.revision: 4
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c51169b12265eea7e6d57e0daa7539322e338851
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>向移动报表添加数据网格 | Reporting Services
有时最佳可视化对象是数据本身。 了解有关这三种*数据网格*，或表，用于显示中的数据[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]:
* 简单数据网格
* 指示器数据网格
* 图表数据网格

## <a name="simple-data-grid"></a>简单数据网格
最基本的简单数据网格可以通过自定义格式和标头显示多个列的数据。 

![mobile-report-simple-data-grid](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

将数据网格添加到设计图面之后，可以将它连接到实际数据。

1. 将从一个简单的数据网格**布局**tab 键移动到设计网格并使其所需的大小。

2. [从 Excel 或共享数据集获取数据](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 选择**数据**选项卡上，然后在**数据属性**窗格中，在**网格视图的数据**选择数据表。

4. 在**列**窗格中，选择所需的列。 重新排列和重命名它们，并设置其格式和聚合。 

 
##  <a name="indicator-data-grid"></a>指示器数据网格
可以向指示器数据网格添加具有仪表的列。

![mobile-report-indicator-data-grid](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. 将从指示器数据网格**布局**tab 键移动到设计网格并使其所需的大小。

2. 上**数据**选项卡中**列**窗格中，选择**添加仪表列**。 

3. 选择**选项**，然后选择**仪表类型**。 

4. 设置**值**和**比较**字段和**值方向**，就如[直接向你的移动报表中添加的仪表](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)。

数据网格会自动向仪表仅馈送特定于该数据网格行的数据。  

## <a name="chart-data-grid"></a>图表数据网格
可以向图表数据网格中添加具有仪表或图表的列。 

![mobile-report-chart-data-grid](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

将图表列添加到数据网格时，需要添加单独的数据表以便为每行中的图表提供数据。 此第二个数据表需要与主数据表共享一个字段，以便将每行链接到其关联图表数据。 

1. 将图表数据网格从**布局**tab 键移动到设计网格并使其所需的大小。

2. 上**数据**选项卡中**列**窗格中，选择**添加图表列**。 

3. [从 Excel 或共享数据集获取数据](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) 以添加与主数据表共享一个字段的第二个数据表（如果尚未这样做）。

4. 下**数据属性**，选择中的主数据表**网格视图的数据**，然后选择在第二个表**图表可视化的引用数据**。

5. 选择**选项**，然后选择**图表类型**。
 
6. 选择**图表数据字段**，**源查找**，和**目标查找**。 
   这三个属性决定了数据网格向列中的每个图表提供数据的方式。
   
   *   **源查找**设置为中的数据表中的字段**网格视图的数据**。 此字段充当按行进行的筛选器，该筛选器应用于图表引用数据表，以便为嵌入式表的每行提供数据。 
   * **目标查找**是中的数据表中的字段**图表可视化的引用数据**。 将在这两个字段对每个行中的图表数据进行联接。   
   * **图表数据字段**确定哪些度量**图表可视化的引用数据**数据表以用作每个行中的图表中的序列的 y 轴值。  

## <a name="see-also"></a>另请参阅 
* [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的导航器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的可视化效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的仪表](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  

