---
title: 计算工具（"计算" 选项卡，多维数据集设计器）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationsview.calculationtoolspane.f1
ms.assetid: b1aa8a1a-6532-45d2-8f53-d3e211d7197a
author: minewiskan
ms.author: owend
ms.openlocfilehash: e658ae7d839a55da315619e0870b32c1da52dad8
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527613"
---
# <a name="calculation-tools-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>计算工具（“计算”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“计算”** 选项卡的 **“计算工具”** 窗格，浏览在计算中可用的元数据、函数和模板。  
  
## <a name="options"></a>选项  
 **元数据**  
 显示所选多维数据集的元数据。  
  
 将所选元素拖到“脚本编辑器”、“计算成员窗体编辑器”或“命名集窗体编辑器”窗格，可以在窗格中的所选位置包括该元素的多维表达式 (MDX) 语法。  
  
 **函数**  
 显示可用于表达式和条件的函数。  
  
 将所选元素拖到 **“脚本编辑器”**、 **“计算成员窗体编辑器”** 或 **“命名集窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
> [!NOTE]  
>  在项目模式下， **“计算工具”** 对话框从随 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供的名为 MDXFunctions.xml 的 XML 文件中读取有关此选项的信息。 在联机模式下，从实例的 MDSCHEMA_FUNCTIONS 架构行集中检索有关此选项的信息。  
  
 **模板**  
 显示可用于计算成员、命名集和脚本命令的预定义模板。  
  
 将所选元素拖到 **“脚本编辑器”**、 **“计算成员窗体编辑器”** 或 **“命名集窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“计算工具”**** 窗格中的元素后，可以从所显示的上下文菜单中访问以下选项：  
  
 **复制**  
 选择此选项可将在 **“元数据”** 或 **“函数”** 中选择的元素复制到剪贴板。  
  
> [!NOTE]  
>   如果选择 **“模板”** ，则不会显示此选项。  
  
> [!NOTE]  
>   如果无法复制所选成员（如 **“元数据”** 中所显示维度的 **“集”** 文件夹，或 **“函数”** 中所显示函数的函数组文件夹），则将禁用此选项。  
  
 **筛选成员**  
 选择此选项可显示 **“筛选成员”** 对话框，并筛选为 **“元数据”** 中所选元素显示的成员。 有关“筛选成员”**** 对话框的详细信息，请参阅[“筛选成员”对话框（Analysis Services - 多维数据）](filter-members-dialog-box-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>   只有在选择了 **“元数据”** 时，才会显示此选项。  
  
> [!NOTE]  
>   只有在 **“元数据”** 中选择了属性的级别时，才会启用此选项。  
  
 **添加模板**  
 选择此选项可根据所选模板将新的计算成员、命名集或脚本命令添加到多维数据集脚本，并显示该命令相应的“脚本编辑器”****、“计算成员窗体编辑器”**** 或“命名集窗体编辑器”****（在窗体视图中），或者在“脚本编辑器”**** 窗格的内容中滚动到多维数据集脚本内该命令的位置（在脚本视图中）。  
  
> [!NOTE]  
>   只有在选择了 **“元数据”** 时，才会显示此选项。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集设计器 &#40;Analysis Services 多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏 &#40;"计算" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [脚本组织程序 &#40;计算 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [计算成员窗体编辑器 &#40;计算 "选项卡、多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](calculated-member-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [命名集窗体编辑器 &#40;计算 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [脚本编辑器 &#40;计算 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [多维数据集设计器&#41; &#40;&#40;计算 Analysis Services 多维数据&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
