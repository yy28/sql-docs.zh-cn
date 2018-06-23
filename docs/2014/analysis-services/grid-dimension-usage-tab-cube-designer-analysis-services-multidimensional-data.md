---
title: 网格 （多维数据集设计器中的维度用法选项卡） (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed63b1da-0fce-4f24-a722-5cff378831e8
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5a470ffb94a457d68b8f47b30b06520984aba87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025527"
---
# <a name="grid-dimension-usage-tab-cube-designer-analysis-services---multidimensional-data"></a>网格（“维度用法”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“维度用法”** 选项卡上的 **“网格”** 窗格，查看和编辑多维数据集维度和度量值组之间的维度关系。 每个维度关系均以网格中的单元来表示，在网格中，度量值组显示为列，而维度则显示为行。  
  
## <a name="options"></a>“常规”  
  
|选项|定义|  
|------------|----------------|  
|**度量值组**|选择要在 **“网格”** 窗格中作为列显示的度量值组。 如果选择“(全部显示)”，将显示所有可用的度量值组。<br /><br /> 单击度量值组的所选列标题可以重命名该度量值组。|  
|**Dimensions**|选择要在 **“网格”** 窗格中作为行显示的多维数据集维度。 如果选择“(全部显示)”，将显示所有可用的多维数据集维度。<br /><br /> 单击维度的所选行标题可以重命名该多维数据集维度。|  
|**（单元）**|选择一个单元格并单击省略号按钮 (**...**) 可显示“定义关系”对话框，以便定义多维数据集维度和度量值组之间的维度关系。 有关“定义关系”对话框的详细信息，请参阅[“定义关系”对话框 (Analysis Services - 多维数据)](define-relationship-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“网格”窗格后，可以从所显示的上下文菜单中访问以下选项：  
  
|选项|定义|  
|------------|----------------|  
|**添加多维数据集维度**|选择此选项可显示 **“添加多维数据集维度”** 对话框，以便添加对多维数据集中的现有或新数据库维度的引用。 有关“添加多维数据集维度”对话框的详细信息，请参阅[“添加多维数据集维度”对话框（Analysis Services - 多维数据）](add-cube-dimension-dialog-box-analysis-services-multidimensional-data.md)。|  
|**新建链接的对象**|选择此选项可显示 **链接对象向导** ，链接来自其他多维数据集的度量值组和维度，并向所选多维数据集导入操作、KPI 和计算。 有关“链接对象向导”的详细信息，请参阅[链接对象向导的 F1 帮助](linked-object-wizard-f1-help.md)。|  
|**剪切**|注意： 将禁用此选项。|  
|**复制**|注意： 将禁用此选项。|  
|**粘贴**|注意： 将禁用此选项。|  
|**删除**|选择此选项可以从多维数据集中删除所选多维数据集维度、度量值组或维度关系。|  
|**重命名**|选择此选项可以重命名所选多维数据集维度、度量值组或维度关系。|  
|**属性**|选择此选项可以在 **中显示所选多维数据集维度、度量值组或维度关系的** “属性” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 窗口。|  
  
## <a name="see-also"></a>请参阅  
 [多维数据集对象&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多维模型中的多维数据集](multidimensional-models/cubes-in-multidimensional-models.md)   
 [维度用法&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;维度使用情况选项卡中，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [维度用法&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)  
  
  