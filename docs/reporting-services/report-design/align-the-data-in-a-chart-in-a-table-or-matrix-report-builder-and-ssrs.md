---
title: 在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d639e686251effc19e445a39c97860a3336c8ff2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581877"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）
  迷你图和数据条是小的简单图表，它们包含一些额外细节，可以传递很多信息。 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，选中此选项时，迷你图和数据条中的值将在表或矩阵的不同单元中对齐，即使缺少它们所基于的数据的值。  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 在此图像中，柱形图显示每个雇员每天的销售额。 请注意，对于雇员没有销售额数据的那些天，该图留空并水平对齐后面的天。 它还通过使不同大小的图表彼此相对，垂直对齐图表。 有关详细信息，请参阅 [迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>对齐迷你图或数据条中的数据  
  
1.  向表或矩阵[添加迷你图或数据条](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) 。  
  
2. 单击迷你图或数据条，然后单击 **“水平轴属性”** 或 **“垂直轴属性”**。  
  
2.  在 **“轴选项”** 选项卡上，选中 **“对齐轴”** 框，然后在下拉框中选择要对齐轴的组。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [添加迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
