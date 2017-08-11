---
title: "将仪表添加到移动报表 |Reporting Services |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ec1f4cee1318947e3c1ab730b3e4f7eaa16dd333
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>向移动报表添加仪表 | Reporting Services
仪表是移动报表中最基本且使用最广泛的视觉对象。 它们显示数据集中的单个值 — 值本身，或相比于目标的值。

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*“布局”选项卡中的仪表可视化效果*  
  
SQL Server 移动报表发布服务器中的所有仪表都具有至少一个属性共同： 一个主要的值，设置其中一个数据表的移动报表中的数字字段。  

除数字仪表外的所有仪表还可以显示比较值或 *差异*值 — 主值和比较值之间的关系。 比较值通常是目标，而仪表是达到该目标的进度或实际值与目标值之间的差异的可视指示器。

仪表只能表示其主值的一个聚合值以及其比较值的一个聚合值。 仪表聚合为标准聚合 — 总和、平均值、最小值、最大值等等。 默认情况下，仪表值为总和，用于显示包含在当前已筛选数据（供仪表控件使用）中的所有值的总计。 

可以通过将仪表值连接到移动报表上的导航器来筛选仪表值。 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>设置仪表的主值和比较值

1. 将从仪表**布局**tab 键移动到设计网格并使其所需的大小。

2. [从 Excel 或共享数据集获取数据](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 选择**数据**选项卡上，然后在**数据属性**窗格中，在**Main 值**选择数据表和数值字段。

3. 在任何仪表除号仪表中**数据属性**窗格中，在**比较值**选择数据表和数值字段。

4. [可选]若要更改的聚合函数，选择**选项**并选择不同的聚合。
   
   >**注意**：当你更改主值的聚合时，可能还想更改比较值的聚合，但在某些情况下，你可能想要混用聚合方法。  

## <a name="filter-a-gauge"></a>筛选仪表
  
如果移动报表有任何导航器，则可以将仪表绑定到其中一个或多个导航器以对其进行筛选。 可以将仪表的值和比较值绑定到一个或多个不同的导航器，从而为仪表提供几乎无限的选项。  

1. 选择仪表，然后在**数据**选项卡中**数据属性**窗格中，选择**选项**旁边**Main 值**或**比较值**。

2. 在“筛选依据”下面选择要筛选仪表的导航器。

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>设置仪表的视觉对象属性
  
除了将仪表元素连接到数据字段的数据属性，还可以自定义多种功能属性和视觉对象属性。 

### <a name="set-value-direction-high-or-low-is-better"></a>设置值方向：值越大越好或值越小越好
* 选择仪表，然后在**布局**选项卡中**Visual 属性**窗格中，设置**值方向**为**值越大越好**或**较低的值是更好**。 

**值越大越好**绿色，指示以更好的理想更改或更低版本正值的颜色值红色，则表示坏结果的不理想更改。 

颜色**较低的值是更好**则正好相反。

值方向属性仅涉及支持比较值的仪表元素。 仪表的颜色由差异整数的符号和值方向属性设置确定。  
  
### <a name="set-range-stops-for-a-gauge"></a>设置仪表的区域停止点
第二项特定于仪表的非数据属性为数据区域停止点。 

* 选择仪表，然后在**布局**选项卡中**Visual 属性**窗格中，选择**范围停止**。

利用区域停止点，可设置应该按比较值的多少百分比将可视化效果呈现为符合目标（绿色）、不确定（琥珀色）或脱离目标（红色）— 仪表的比较值为目标。 同样，只有具有比较值的仪表才支持区域停止点。  

### <a name="format-the-numbers-in-the-gauge"></a>格式化仪表中的数字  
仪表元素的另一非数据属性（也是供许多其他元素共享的属性）为数字格式。 

* 选择仪表，然后在**布局**选项卡中**Visual 属性**窗格中，选择**范围停止**。

它决定了如何格式化仪表中显示的数字，例如，货币、百分比、时间或常规。 可对移动报表的每个元素设置数字格式。
  
### <a name="see-also"></a>另请参阅 

* [使用 SQL Server 移动报表发布服务器创建移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的导航器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的可视化效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 移动报表中的数据网格](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 

