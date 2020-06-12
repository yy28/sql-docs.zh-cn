---
title: 计算工具（"操作" 选项卡，多维数据集设计器）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
author: minewiskan
ms.author: owend
ms.openlocfilehash: 42336656ce19d36cf0eadc986450dd8f3b81f669
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527640"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>计算工具（“操作”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“操作”** 选项卡上的 **“计算工具”** 窗格，浏览在操作、钻取操作和报表操作中可用的元数据、函数和模板。  
  
## <a name="options"></a>选项  
 **元数据**  
 显示所选多维数据集的元数据。  
  
 将所选元素拖到“操作窗体编辑器”****、“钻取操作窗体编辑器”**** 或“报表操作窗体编辑器”**** 窗格，可以在窗格中的所选位置包括该元素的多维表达式 (MDX) 语法。  
  
 **函数**  
 显示可用于表达式和条件的函数。  
  
 将所选元素拖到 **“操作窗体编辑器”**、 **“钻取操作窗体编辑器”** 或 **“报表操作窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
> [!NOTE]  
>  在项目模式下， **“计算工具”** 对话框从随 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供的名为 MDXFunctions.xml 的 XML 文件中读取有关此选项的信息。 在联机模式下，从实例的 MDSCHEMA_FUNCTIONS 架构行集中检索有关此选项的信息。  
  
 **模板**  
 显示可用于操作的预定义模板。  
  
 将所选元素拖到 **“操作窗体编辑器”**、 **“钻取操作窗体编辑器”** 或 **“报表操作窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“计算工具”**** 窗格中的元素后，可以从所显示的上下文菜单中访问以下选项：  
  
|选项|定义|  
|------------|----------------|  
|**复制**|选择此选项可将在 **“元数据”** 或 **“函数”** 中选择的元素复制到剪贴板。<br /><br /> 请注意，如果选择 "**模板**"，则不会显示此选项。 另请注意，如果无法复制所选成员（例如，在**元数据**中显示维度的 "**集**" 文件夹，或**函数中显示**函数的函数组文件夹），则将禁用此选项。|  
|**筛选成员**|选择此选项可显示 **“筛选成员”** 对话框，并筛选为 **“元数据”** 中所选元素显示的成员。 有关“筛选成员”**** 对话框的详细信息，请参阅[“筛选成员”对话框（Analysis Services - 多维数据）](filter-members-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 请注意，只有在选择了 "**元数据**" 时，才会显示此选项。 另请注意，只有在 "**元数据**" 中选择了属性的级别时，才会启用此选项。|  
|**添加模板**|选择此选项可以基于所选模板，将新的操作、钻取操作或报表操作添加到多维数据集，并分别显示 **操作窗体编辑器**、 **钻取操作窗体编辑器**或 **报表操作窗体编辑器**。<br /><br /> 注意：只有在选择了 "**元数据**" 时，才会显示此选项。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 脚本编写基础 &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [&#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据的操作&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [操作管理器 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [操作窗体编辑器 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [钻取操作窗体编辑器 &#40;操作 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [报表操作窗体编辑器 &#40;操作 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
