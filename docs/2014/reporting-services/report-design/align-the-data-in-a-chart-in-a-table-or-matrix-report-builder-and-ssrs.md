---
title: 在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 74b6e86e6c9e7fd9d293e4c1bdab952468adb4b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106512"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）
  迷你图和数据条是小的简单图表，它们包含一些额外细节，可以传递很多信息。 选中此选项时，迷你图和数据条中的值将在表或矩阵的不同单元中对齐，即使缺少它们所基于的数据的值。  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 在此图像中，柱形图显示每个雇员每天的销售额。 请注意，对于雇员没有销售额数据的那些天，该图留空并水平对齐后面的天。 它还通过使不同大小的图表彼此相对，垂直对齐图表。 有关详细信息，请参阅 [迷你图和数据条（报表生成器和 SSRS）](sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="align-the-data-in-a-sparkline-or-data-bar"></a>对齐迷你图或数据条中的数据  
  
1.  单击迷你图或数据条，然后单击 **“水平轴属性”** 或 **“垂直轴属性”**。  
  
2.  在 **“轴选项”** 选项卡上，选中 **“对齐轴”** 框，然后在下拉框中选择要对齐轴的组。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [&#40;报表生成器和 SSRS 添加迷你图和数据条&#41;](add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
