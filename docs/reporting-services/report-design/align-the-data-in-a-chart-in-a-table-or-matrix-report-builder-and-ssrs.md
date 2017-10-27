---
title: "对齐表或矩阵 （报表生成器和 SSRS） 中的图表中的数据 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d64ebc0ee2345088419e44ab819c0d94d26274a8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）
  迷你图和数据条是小的简单图表，它们包含一些额外细节，可以传递很多信息。 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，选中此选项时，迷你图和数据条中的值将在表或矩阵的不同单元中对齐，即使缺少它们所基于的数据的值。  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 在此图像中，柱形图显示每个雇员每天的销售额。 请注意，对于雇员没有销售额数据的那些天，该图留空并水平对齐后面的天。 它还通过使不同大小的图表彼此相对，垂直对齐图表。 有关详细信息，请参阅[迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>对齐迷你图或数据条中的数据  
  
1.  向表或矩阵[添加迷你图或数据条](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) 。  
  
2. 单击迷你图或数据条，然后单击 **“水平轴属性”** 或 **“垂直轴属性”**。  
  
2.  在 **“轴选项”** 选项卡上，选中 **“对齐轴”** 框，然后在下拉框中选择要对齐轴的组。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [添加迷你图和数据条 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  

