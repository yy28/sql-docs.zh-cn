---
title: 计算成员窗体编辑器 （计算选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a16319b01c6555aa3bf299da201d9662cd59f4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667857"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>计算成员窗体编辑器（“计算”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“计算”** 选项卡上的 **“计算成员窗体编辑器”** 窗格创建或修改计算成员。  
  
 **注意** 此窗格仅显示在窗体视图中。  
  
## <a name="options"></a>选项  
 **名称**  
 键入计算成员的名称。  
  
 **父属性**  
 展开此项可以查看“父层次结构”、“父成员”和“更改”选项。  
  
 **父层次结构**  
 在选定的多维数据集中选择要包含计算成员的维度和层次结构。 选择 MEASURES 可以定义计算度量值。  
  
 **父成员**  
 选择在其下面将显示计算成员的成员。  
  
 **注意** 只有在 **“父层次结构”** 指定了 MEASURES 以外的层次结构时，此选项才可用。  
  
 **更改**  
 选择此项可以显示“选择父成员”对话框并为“父成员”选择成员。 有关“选择父成员”对话框的详细信息，请参阅[“选择父成员”对话框（Analysis Services - 多维数据）](select-parent-member-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **表达式**  
 展开此项可以查看或编辑计算成员的多维表达式 (MDX) 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
> [!NOTE]  
>  建议此表达式的计算结果为字符串或数值。  
  
 **附加属性**  
 展开此项可以查看“格式字符串”、“可见”、“非空行为”、“颜色表达式”和“字体表达式”选项。  
  
 **格式字符串**  
 键入用于对计算成员所返回的值进行格式设置的 MDX 格式字符串，或选择预定义的格式字符串。  
  
 有关 MDX 格式字符串的详细信息，请参阅 [FORMAT_STRING 内容 (MDX)](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)。  
  
 **Visible**  
 选择 **True** 将允许计算成员对客户端应用程序可见。  
  
 **非空行为**  
 选择用于为计算成员解析 MDX 中的 NON EMPTY 查询的度量值名称。 如果 **“非空行为”** 属性为空白，则必须对计算成员进行反复计算以确定成员是否为空。 如果 **“非空行为”** 属性包含度量值的名称，则在指定的度量值为空的情况下将计算成员视为空。  
  
> [!WARNING]  
>  不推荐使用此属性。 避免将其设置。 请参阅[SQL Server 2014 中不推荐使用 Analysis Services 功能](deprecated-analysis-services-features-in-sql-server-2014.md)有关详细信息。  
  
 **颜色表达式**  
 展开此项可以查看“前景色”和“背景色”选项。  
  
 **前景色**  
 键入提供计算成员的前景色的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 单击颜色选择按钮可显示“颜色”对话框，使用该对话框可以向 MDX 表达式中插入指定颜色的 RGB（红-绿-蓝）值。 有关 RGB 值的详细信息，请参阅 [FORE_COLOR 和 BACK_COLOR 内容 (MDX)](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。  
  
 **背景色**  
 键入提供计算成员的背景色的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 单击颜色选择按钮可显示“颜色”对话框，使用该对话框可以向 MDX 表达式中插入指定颜色的 RGB（红-绿-蓝）值。 有关 RGB 值的详细信息，请参阅 [FORE_COLOR 和 BACK_COLOR 内容 (MDX)](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。  
  
 **字体表达式**  
 展开此项可以查看“字体名称”、“字号”和“字体标志”选项。  
  
 **字体名称**  
 键入提供计算成员所用字体名称的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 单击字体选择按钮可显示 **“字体”** 对话框，使用该对话框可以向 MDX 表达式中插入指定字体的属性值。 有关属性值的详细信息，请参阅[创建和使用属性值 (MDX)](creating-and-using-property-values-mdx.md)。  
  
 **字号**  
 键入提供计算成员所用字体大小的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 单击字体选择按钮可显示 **“字体”** 对话框，使用该对话框可以向 MDX 表达式中插入指定字体的属性值。 有关属性值的详细信息，请参阅[创建和使用属性值 (MDX)](creating-and-using-property-values-mdx.md)。  
  
 **字体标志**  
 键入提供计算成员所用字体的位图化值（包含下划线或加粗等之类的字体标志）的 MDX 表达式。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 单击字体选择按钮可显示 **“字体”** 对话框，使用该对话框可以向 MDX 表达式中插入指定字体的属性值。 有关属性值的详细信息，请参阅[创建和使用属性值 (MDX)](creating-and-using-property-values-mdx.md)。  
  
## <a name="see-also"></a>请参阅  
 [计算](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [创建计算的成员](multidimensional-models/create-calculated-members.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [计算&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;计算选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [脚本组织程序&#40;计算选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [计算工具&#40;计算选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [命名集窗体编辑器&#40;计算选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [脚本编辑器&#40;计算选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
