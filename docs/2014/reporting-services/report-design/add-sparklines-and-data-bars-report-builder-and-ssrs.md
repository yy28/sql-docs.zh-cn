---
title: 添加迷你图和数据条（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0b297c2e-d48b-41b0-aabd-29680cdcdb05
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e95e9543cb3eb1efdc0f7a1589133f5691a9fd33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028518"
---
# <a name="add-sparklines-and-data-bars-report-builder-and-ssrs"></a>添加迷你图和数据条（报表生成器和 SSRS）
  迷你图和数据条是小的备用图，它包含一些额外细节，可以传递很多信息。 有关它们的详细信息，请参阅[迷你图和数据条（报表生成器和 SSRS）](sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
 迷你图和数据条在表或矩阵的单元中最常见。 迷你图通常每个只显示一个系列。 数据条可以包含一个或多个数据点。 迷你图和数据条都是通过重复表或矩阵中每行的序列信息来得出它们的影响。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-sparkline-or-data-bar-to-a-table-or-matrix"></a>向表或矩阵添加迷你图或数据条  
  
1.  如果还没有这样做，请使用要显示的数据创建一个表或矩阵。 有关详细信息，请参阅[表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)或[矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)。  
  
2.  在您的表或矩阵中插入列。 有关详细信息，请参阅[插入或删除列（报表生成器和 SSRS）](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **“插入”** 选项卡上，单击 **“迷你图”** 或 **“数据条”**，然后单击新列中的单元。  
  
    > [!NOTE]  
    >  不能将迷你图放置于表的详细信息组中。 它们必须处于与组相关联的单元中。  
  
4.  在“更改迷你图/数据条类型”对话框中，单击所需的迷你图或数据条类型，然后单击“确定”。  
  
5.  单击该迷你图或数据条。  
  
     将打开 **“图表数据”** 窗格。  
  
6.  在“值”区域中，单击“添加字段”加号 (**+**)，然后单击要将其值制成图表的字段。  
  
7.  在“类别组”区域中，单击“添加字段”加号 (**+**)，然后单击要依据其值分组的字段。  
  
     对于迷你图和数据条，通常不向 **“序列组”** 区域添加字段，因为每行只需要一个序列。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [对齐表或矩阵中的图表中的数据&#40;报表生成器和 SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  