---
title: 将 HTML 导入报表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dd0410ea-8839-4e8c-9944-8cdfe5465591
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a90dfbac3006f7dfbf27b38a8ab584ebb9e5d710
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249627"
---
# <a name="importing-html-into-a-report-report-builder-and-ssrs"></a>将 HTML 导入报表（报表生成器和 SSRS）
  可以使用文本框向报表中插入从数据集字段中检索到的 HTML 格式的文本。 文本可以来自于其计算结果为正确格式的 HTML 的任何简单或复杂表达式。 格式化文本可以呈现为支持的所有输出格式，包括 PDF。  
  
 ![rs_HTMLFormatting](../media/rs-htmlformatting.gif "rs_HTMLFormatting")  
  
 下图显示了在报表设计视图中显示 HTML 格式的文本，以及在运行报表时所呈现的相同文本。  
  
> [!NOTE]  
>  导入包含 HTML 标记的文本时，文本框必须始终首先分析数据。 由于仅支持 HTML 标记的子集，因此在呈现报表中显示的 HTML 可能不同于您的原始 HTML。  
  
 若要快速开始使用，请参阅[教程：设置文本格式（报表生成器）](../tutorial-format-text-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="supported-html-tags"></a>支持的 HTML 标记  
 以下是作为占位符文本定义时将呈现为 HTML 标记的完整列表：  
  
-   标头、 样式和块元素： \<H {n} >， \<d i V >， \<s p a N >，\<P >， \<l I >  
  
 在报表处理期间，将忽略任何其他 HTML 标记。 如果占位符文本中表达式所表示的 HTML 格式不正确，则将占位符呈现为纯文本。 所有 HTML 标记都不区分大小写。  
  
 如果文本框中的文本仅包含一个文本块，将以正确方式呈现占位符中用于定义块元素的任何 HTML。 但是，如果文本框具有多个文本块，则忽略 HTML 标记，并通过文本块定义文本结构。  
  
 如果为文本定义了一个以上的标记，并且 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 检测到 HTML 与现有报表约束冲突，则只有最内部的 HTML 标记被视为 HTML。  
  
 使用列表处理标签时，所有项目符号和数字前缀的字体和样式都固定采用 Arial 黑色。  
  
 有关详细信息，请参阅[向报表添加 HTML（报表生成器和 SSRS）](add-html-into-a-report-report-builder-and-ssrs.md)。  
  
## <a name="limitations-of-cascading-style-sheet-attributes"></a>级联样式表属性的限制  
 使用级联样式表 (CSS) 属性时，仅定义一组基本标记。 以下是支持的属性列表：  
  
-   text-align、text-indent  
  
-   font-family  
  
-   font-size  
  
    -   仅支持采用绝对 CSS 长度单位的有效 RDL 大小值。 支持的单位为：in、cm、mm、pt、pc。  
  
    -   忽略相对 CSS 长度单位，不支持它们。 不支持的单位包括 em、ex、px、%、rem。  
  
     有关 CSS 单位的详细信息，请参阅：[CSS 值和单位参考](http://msdn.microsoft.com/en-us/library/ms531211\(VS.85\).aspx) (http://msdn.microsoft.com/library/ms531211(VS.85).aspx)。  
  
-   color  
  
-   padding、padding-bottom、padding-top、padding-right、padding-left  
  
-   font-weight  
  
 以下是使用 CSS 的一些注意事项：  
  
-   格式不正确的 CSS 值和 HTML 的忽略方式相同。  
  
-   如果同一标记中存在特性和 CSS 样式特性，则 CSS 属性具有较高优先级。 例如，如果文本为 \<p style="text-align: right" align="left">，则仅应用 text-align 特性，并且文本为右对齐。  
  
-   对于特性和 CSS 样式，如果多次指定某一属性，则仅应用该属性的最后一个实例。 例如，如果文本为 \<p align="left" align="right">，该文本则为右对齐。  
  
## <a name="see-also"></a>请参阅  
 [以 html 格式呈现&#40;报表生成器和 SSRS&#41;](../report-builder/rendering-to-html-report-builder-and-ssrs.md)  
  
  
