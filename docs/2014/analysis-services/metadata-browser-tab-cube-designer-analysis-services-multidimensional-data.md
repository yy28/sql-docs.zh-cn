---
title: 元数据 （浏览器选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c14a039d22238450023c4a7f9b7b099e9a2a53
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171147"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>元数据（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  在多维数据集设计器中，可以使用 **“浏览器”** 选项卡上的 **“元数据”** 窗格浏览多维数据集的结构，以查看相关度量值，以及查看和创建维度。 您可以深化到层次结构中，查看可用度量值和 KPI 的列表，并复制对象的完全限定名称。  
  
 还可以将 **“元数据”** 窗格中的对象和层次结构拖至查询生成区域，以创建新查询或导出数据以便在 Excel 中浏览。  
  
## <a name="options"></a>选项  
 **元数据**  
 显示当前视图中可用的元数据。 可以更改该视图（即当前选定的透视或多维数据集），只需单击多维数据集图标，然后使用“选择多维数据集”对话框选择新的多维数据集或透视。 还可以单击 **“度量值组”**，然后从下拉列表中选择新的度量值组，以便筛选在 **“元数据”** 窗格中可用的对象。  
  
 将所选项拖到 [!INCLUDE[msCoName](../includes/msconame-md.md)] “报表” **窗格中的** Office 11.0 数据透视表控件的筛选器、数据、行或列区域中，可以显示所选项的数据。  
  
 **函数**  
 显示可用于在“浏览器”中创建查询或数据视图的所有函数、运算符和常量的列表。 若要使用某个函数，找到所需的函数，然后将其拖入查询区域。 语法定义将添加到文本中。  
  
> [!WARNING]  
>  在图形设计视图中工作时，“函数”列表不可用。  
  
 当使用表格模型时，函数列表将包含 MDX 函数和 DAX 函数。 否则，该列表仅包含 MDX。 多维模型无法直接使用 DAX 函数，尽管可以在对象定义中包括 DAX 表达式。  
  
 提示：包含 DAX 函数的文件夹以全大写字母列出。 所有其他文件夹包含的都是 MDX 函数。 例如，有两个用于统计函数的文件夹： **STATISTICAL** 包含相关的 DAX 函数。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“元数据”窗格中显示的元素，可以从所显示的上下文菜单中访问以下选项：  
  
|选项|Description|  
|------------|-----------------|  
|**将添加到查询**|单击此选项可以将选定的对象添加到查询生成区域的下部窗格中。|  
|**添加到筛选器**|单击此选项可以将所选的维度、属性、层次结构或级别添加至 **“浏览器”** 的筛选区域。<br /><br /> 注意：只有在选择了维度、属性、层次结构或级别时，才会启用此选项。|  
|**复制**|单击此选项可以将所选项添加到剪贴板。<br /><br /> 注意：此选项复制对象的完全限定名称。|  
  
## <a name="see-also"></a>请参阅  
 [工具栏&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [在 Excel 中分析&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [查询和筛选器&#40;浏览器选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [浏览器&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
