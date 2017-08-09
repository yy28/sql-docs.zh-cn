---
title: "在移动报表中的行或列中的数据分组 |Reporting Services |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c1b584f5a88af5055ffac67932fd94a37734bfd
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="group-data-by-columns-or-rows-in-a-mobile-report--reporting-services"></a>在移动报表中按列或行对数据进行分组 | Reporting Service
在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]中的许多类型的图表中，可以按列或按行来组织数据。 按照此分步说明执行操作。

在时间图、总计图、饼图和漏斗图，可以按行或按列来组织数据。 
* 如果表包含几列要进行比较的数据，则按列进行组织会很有用。 
* 如果表中的一列包含不同类别的名称，则按行进行组织会效果更好。 

以下步骤在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 中使用具有模拟数据的比较总计表来演示在图表中按行或按列来构建数据结构之间的差异。  

1. 将**比较总计图**从“布局”选项卡拖动到设计图面并扩大它。

2. 选择“数据”选项卡。 你会看到 SimulatedTable 表包含一系列的列，即 **Metric1** 到 **Metric5**，以及 **Comparison1** 到 **Comparison5**。 

   ![mobile-report-data-group-column](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. 在“数据属性”窗格中，“主系列”是 **SimulatedTable**。 选择“主系列”旁的框中的箭头，会看到 **Metric1** 到 **Metric5** 处于选择状态。

   ![mobile-report-properties-columns](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   “比较系列”也是同样情况   -- **Comparison1** 到 **Comparison5** 处于选择状态。
   
4. 选择“预览”。

   ![mobile-report-chart-by-columns](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   图表中的每条都表示表中的一列。 较粗条是“度量”列，较细条是“比较”列。

5. 选择左上角的向后箭头以离开预览模式。

6. 在“布局”选项卡上的“视觉属性”窗格中，将“数据结构”从“按列”更改为“按行”。  

7. 选择“数据”选项卡。 现在 SimulatedTable 表具有一个“类别”列以及“度量”和“比较”列（类别 A 到 E）。 

   ![mobile-report-data-group-rows](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  在“数据属性”窗格中，现在有一个“类别列”框，其中列出了 SimulatedTable 中的“类别”列。 在“主系列”中，可以选取要用于值的列。 默认情况下， [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 会为“主系列”选择 Metric5 到 Metric1，为“比较系列”选择 Comparison1 到 Comparison5。 

    ![mobile-report-properties-rows](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. 选择“预览”。

   ![mobile-report-chart-by-rows](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   现在图表中的每条都表示“类别”列中每种类别的值。

### <a name="see-also"></a>另请参阅
* [Reporting Services 移动报表中的可视化效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
