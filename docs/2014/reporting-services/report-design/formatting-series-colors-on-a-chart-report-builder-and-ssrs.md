---
title: 设置图表上序列颜色的格式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10245"
- "10252"
- sql12.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql12.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3f3622ea10c5dbd0b38e7562ec8039fb1f28571b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298165"
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>设置图表上序列颜色的格式（报表生成器和 SSRS）
  Reporting Services 为图表提供了多种内置调色板，或者您也可以定义自定义调色板。 默认情况下，图表使用内置**BrightPastel**颜色调色板填充每个序列。 这些颜色也会显示在图例中。 向图表添加多个序列时，图表按颜色在调色板中的定义顺序为序列各分配一种颜色。  
  
 如果序列中的颜色数多于调色板中的颜色，图表将开始重用颜色，因此两个序列可能具有相同的颜色。 如果使用的是形状图，形状图中的每个数据点都分配有调色板中的颜色，因此可能经常发生这种情况。 为避免混淆，请将自定义调色板的颜色数至少定义为图表上的相同序列数。  
  
 可以选择新调色板，也可以从“属性”窗格定义自定义调色板。 有关详细信息，请参阅[使用调色板定义图表上的颜色（报表生成器和 SSRS）](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>使用内置调色板  
 Reporting Services 提供了一系列可用于为图表上的序列定义颜色集的预定义内置调色板。 所有内置调色板包含 10 至 16 种颜色值。 无法扩展内置调色板使其包括更多颜色，因此如果需要的颜色超过 16 种，必须定义自定义调色板。  
  
 如果要打印报表，请考虑使用 **“灰度”** 调色板。 该调色板使用多种色度的黑色和白色来表示图表中的每个序列。  
  
 名为“默认”的调色板在 Reporting Services 早期版本中用作默认图表调色板。 该调色板使用相同名称进行维护以保持一致。 图表将使用默认调色板进行无缝升级，但在升级之后，可以考虑更改它。  
  
## <a name="using-custom-palettes"></a>使用自定义调色板  
 如果要向图表应用您自己的颜色，请使用自定义调色板。 使用自定义调色板可以按颜色在图表上的所需显示顺序来添加您自己的颜色。 如果在设计时不知道图表中的序列数，使用自定义调色板尤其有用。 有关详细信息，请参阅[使用调色板定义图表上的颜色（报表生成器和 SSRS）](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)。  
  
## <a name="using-a-color-fill-on-each-series"></a>对每个序列使用颜色填充  
 通过为图表中的每个序列各指定一种颜色，还可以在图表上定义您自己的颜色。 为此，请打开 **“序列属性”** 对话框，并设置 **“填充”** 的 **“颜色”** 属性。 该方法将覆盖定义的所有调色板。 通常，最好使用自定义调色板定义您自己的颜色，因为在报表处理之前，您可能不知道数据集中的序列数。  
  
 该方法最适合希望根据表达式按条件设置序列颜色的情况。  有关详细信息，请参阅 [设置图表上数据点的格式（报表生成器和 SSRS）](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [对多个形状图指定一致的颜色（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)  
  
 [使用调色板定义图表上的颜色（报表生成器和 SSRS](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)）  
  
 [通过添加条带线突出显示图表数据（报表生成器和 SSRS）](highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>请参阅  
 [设置图表格式（报表生成器和 SSRS）](formatting-a-chart-report-builder-and-ssrs.md)   
 [向图表添加凹凸效果、阳文和纹理样式（报表生成器和 SSRS）](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)   
 [设置图表上图例的格式（报表生成器和 SSRS）](chart-legend-formatting-report-builder.md)  
  
  
