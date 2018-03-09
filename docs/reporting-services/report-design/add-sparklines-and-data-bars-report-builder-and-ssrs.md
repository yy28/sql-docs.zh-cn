---
title: "添加迷你图和数据条（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 20f192f6480b392e611f875c85d0f65d9dc639b4
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>添加迷你图和数据条（报表生成器和 SSRS）
  迷你图和数据条是小的备用图，它包含一些额外细节，可以传递很多信息。 有关它们的详细信息，请参阅[迷你图和数据条（报表生成器和 SSRS）](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，迷你图和数据条最常见于表或矩阵的单元中。 迷你图通常每个只显示一个系列。 数据条可以包含一个或多个数据点。 迷你图和数据条都是通过重复表或矩阵中每行的序列信息来得出它们的影响。  
  
## <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>向表或矩阵添加迷你图或数据条  
  
1.  如果还没有这样做，请使用要显示的数据创建一个 [表](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) 或 [矩阵](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md) 。  
  
2.  在您的表或矩阵中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 选项卡上，单击 **“迷你图”** 或 **“数据条”**，然后单击新列中的单元。  
  
    > [!NOTE]  
    >  不能将迷你图放置于表的详细信息组中。 它们必须处于与组相关联的单元中。  
  
4.  在“更改迷你图/数据条类型”对话框中，单击所需的迷你图或数据条类型，然后单击“确定”。  
  
5.  单击该迷你图或数据条。  
  
     将打开 **“图表数据”** 窗格。  
  
6.  在“值”区域中，单击“添加字段”加号 (**+**)，然后单击要将其值制成图表的字段。  
  
7.  在“类别组”区域中，单击“添加字段”加号 (**+**)，然后单击要依据其值分组的字段。  
  
     对于迷你图和数据条，通常不向 **“序列组”** 区域添加字段，因为每行只需要一个序列。  
  
## <a name="see-also"></a>另请参阅  
 [图表（报表生成器和 SSRS）](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [在表或矩阵中的图表中对齐数据（报表生成器和 SSRS）](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
