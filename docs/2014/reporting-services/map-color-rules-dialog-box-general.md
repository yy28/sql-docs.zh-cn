---
title: 地图颜色规则对话框，常规 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10541"
- sql12.rtp.rptdesigner.shared.mapcolorrulesgeneral.f1
ms.assetid: 14ff5fc1-4cf8-4a45-9d98-47a1bf1c52c4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e97de85cdd57fdb21aa82379243eb6954358ea38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108323"
---
# <a name="map-color-rules-dialog-box-general"></a>“地图颜色规则”对话框 -&gt;“常规”
  选择 **“颜色规则属性”** 对话框中的 **“常规”** 可以定义此层上地图元素的颜色选项。 地图元素包括多边形、线条和点。 当您创建了基于空间数据的地图元素和来自数据集字段（或来自空间数据源字段）的分析数据之间的关系后，就可以应用颜色规则。  
  
 若要通过指定具有不同主要颜色和辅助颜色的装饰性渐变来显示层上的所有地图元素，请使用“地图多边形属性”对话框的 **“填充”** 页。 对于层来说，颜色规则优先于显示属性。 有关详细信息，请参阅[自定义地图或地图层的数据和显示（报表生成器和 SSRS）](report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>选项  
 **应用模板样式**  
 选择此选项可以基于主题使用颜色，该主题在向导中选择或在“多边形”、“线条”或“点”层属性中设置。 主题为地图的颜色、字体和边框设置默认选项。 对于此选项，不应用任何规则来将颜色分配给每个地图元素。  
  
 **使用调色板实现数据可视化效果**  
 选择此选项可以使用特定调色板中的颜色来将分析数据可视化。  
  
 **通过使用颜色范围实现数据可视化**  
 选择此选项可以使用每个地图元素的颜色范围来将分析数据可视化。 例如，当您指定“红”作为开始颜色、“黄”作为中间颜色以及“绿”作为结束颜色时，在低范围中的值将为“红”，在中间范围中的值将为“黄”，在高范围中的值将为“绿”。  
  
 **通过使用自定义颜色实现可视化数据**  
 选择此选项可以通过指定您自己的颜色列表来将分析数据可视化。  
  
 **数据字段**  
 选择 **“实现数据的可视化效果”** 选项之一时，将显示此选项。  
  
 从下拉列表中选择要使用的分析数据字段。 根据空间数据的来源不同，该列表显示来自空间数据源的字段或具有空间数据和分析数据之间的某一对应关系的报表数据集的字段。 若要创建这样的关系，请在所选地图层的“分析数据”页上设置数据选项。  
  
 **Palette**  
 键入或选择调色板的名称。  
  
 **开始颜色**  
 指定处于数据范围低端的数据要使用的颜色。  
  
 **中间颜色**  
 指定处于数据范围中部的数据要使用的颜色。 选择 **“无颜色”** 可以删除此范围。  
  
 **结束颜色**  
 指定处于数据范围高端的数据要使用的颜色。  
  
 **“添加”**  
 单击 **“添加”** 可以为颜色规则指定您自己的颜色。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)   
 [更改地图图例、色阶和关联的规则（报表生成器和 SSRS）](report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)  
  
  
