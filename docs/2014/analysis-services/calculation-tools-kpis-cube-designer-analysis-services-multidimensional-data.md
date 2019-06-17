---
title: 计算工具 （Kpi 选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpisview.calculationtoolspane.f1
ms.assetid: c030c725-7763-4c23-9988-4b274a88fc31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd16965c81ccb091d70320bd91c56112d3c15a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088273"
---
# <a name="calculation-tools-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>计算工具（KPI 选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集中的“KPI”  选项卡上的“计算工具”  窗格，浏览在关键绩效指标 (KPI) 中可用的元数据、函数和模板。  
  
> [!NOTE]  
>  此窗格仅显示在窗体视图中。  
  
## <a name="options"></a>选项  
 **元数据**  
 显示所选多维数据集的元数据。  
  
 将所选元素拖到  “KPI 窗体编辑器”窗格，可以在窗格中的所选位置包括该元素的多维表达式 (MDX) 语法。  
  
 **函数**  
 显示可用于表达式和条件的函数。  
  
 将所选元素拖到 **“KPI 窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
> [!NOTE]  
>  在项目模式下， **“计算工具”** 对话框从随 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]提供的名为 MDXFunctions.xml 的 XML 文件中读取有关此选项的信息。 在联机模式下，从实例的 MDSCHEMA_FUNCTIONS 架构行集中检索有关此选项的信息。  
  
 **模板**  
 显示可用于 KPI 的预定义模板。  
  
 将所选元素拖到 **“KPI 窗体编辑器”** 窗格，可以在窗格中的所选位置包括该元素的 MDX 语法。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“计算工具”  窗格中的元素后，可以从所显示的上下文菜单中访问以下选项：  
  
 **复制**  
 选择此选项可将在 **“元数据”** 或 **“函数”** 中选择的元素复制到剪贴板。  
  
> [!NOTE]  
>  如果选择 **“模板”** ，则不会显示此选项。  
  
> [!NOTE]  
>  如果无法复制所选成员（如 **“元数据”** 中所显示维度的 **“集”** 文件夹，或 **“函数”** 中所显示函数的函数组文件夹），则将禁用此选项。  
  
 **筛选成员**  
 选择此选项可显示 **“筛选成员”** 对话框，并筛选为 **“元数据”** 中所选元素显示的成员。 有关“筛选成员”  对话框的详细信息，请参阅[“筛选成员”对话框（Analysis Services - 多维数据）](filter-members-dialog-box-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  只有在选择了 **“元数据”** 时，才会显示此选项。  
  
> [!NOTE]  
>  只有在 **“元数据”** 中选择了属性的级别时，才会启用此选项。  
  
 **添加模板**  
 选择此选项可以基于所选模板向多维数据集脚本中添加新的计算成员、命名集或者脚本命令，并以窗体视图显示“KPI 窗体编辑器”  。  
  
> [!NOTE]  
>  只有在选择了 **“元数据”** 时，才会显示此选项。  
  
## <a name="see-also"></a>请参阅  
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Kpi&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;Kpi 选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 组织程序&#40;Kpi 选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpi-organizer-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 窗体编辑器&#40;Kpi 选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpi-form-editor-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [KPI 浏览器&#40;Kpi 选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpi-browser-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
