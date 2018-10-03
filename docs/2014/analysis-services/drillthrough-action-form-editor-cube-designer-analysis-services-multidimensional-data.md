---
title: 钻取操作窗体编辑器 （操作选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8589c743e926b6654cfba123ef7a47a85c0e95d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213227"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>钻取操作窗体编辑器（“操作”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“操作”** 选项卡上的 **“钻取操作窗体编辑器”** 窗格，修改在 **“操作组织程序”** 窗格中选择的钻取操作。 有关钻取操作的详细信息，请参阅[操作（Analysis Services - 多维数据）](multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  钻取操作不再深化到基础数据存储区。 必须使用维度或层次结构成员在多维数据集中对钻取操作访问的信息进行建模。  
  
## <a name="options"></a>选项  
 **名称**  
 键入操作的名称。  
  
 **操作目标**  
 展开可查看“度量值组成员”选项。  
  
 **度量值组成员**  
 选择要与钻取操作关联的度量值组。  
  
 **条件(可选)**  
 输入描述可选条件（与“度量值组成员”一起使用）的多维表达式 (MDX) 表达式，以进一步限制操作可用的时间。 表达式必须返回一个布尔值，如果为 True，指示该操作可用。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **钻取列**  
 展开可显示一个网格，指示在用户运行此操作时返回的属性。  
  
> [!NOTE]  
>  您可以选择多个维度，但在钻取操作中每个维度只能使用一次。  
  
 该网格包含以下列：  
  
|“列”|Description|  
|------------|-----------------|  
|**Dimensions**|选择派生所返回属性的维度。 选择 MEASURES 可以钻取度量值。|  
|**返回列**|从所选维度中选择将在操作运行时返回的属性或度量值。|  
  
 **附加属性**  
 展开可查看“默认值”、“最大行数”、“调用”、“应用程序”、“说明”、“标题”和“标题是 MDX”选项。  
  
 **Default**  
 若要将此钻取操作设置为默认的钻取操作，请选择 **True** ，否则选择 **False**。  
  
 如果`RETURN`省略子句的 mdx`DRILLTHROUGH`由客户端应用程序，执行语句[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例评估所有默认钻取操作，并运行第一个默认钻取返回非空的集合的操作。 有关 MDX 的详细信息`DRILLTHROUGH`语句，请参阅[钻取语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough)。  
  
> [!NOTE]  
>  使用此选项只是为了向后兼容。  
  
 **最大行数**  
 键入钻取操作返回的最大行数。 将此选项设置为零或空值表示钻取操作将向客户端应用程序返回该操作检索到的所有行。  
  
 **调用**  
 选择相应设置，指示何时执行该操作。  
  
> [!NOTE]  
>  此选项只是向客户端应用程序提供何时执行某项操作的建议，并不直接控制对该操作的调用。  
  
 下表对可用的设置进行了说明：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|批处理|该操作将作为批处理操作或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 任务的一部分运行。|  
|交互|在用户调用该操作时运行。|  
|处于打开状态|第一次打开多维数据集时运行该操作。|  
  
 **应用程序**  
 键入可执行钻取操作的应用程序的名称。  
  
 还可以使用此选项来标识最常使用此操作的客户端应用程序，并在弹出菜单中该操作的旁边显示相应的图标。  
  
> [!NOTE]  
>  此选项只是向客户端应用程序提供使用哪一个客户端应用程序执行某项操作的建议，并不直接控制对该操作的访问。 客户端应用程序将隐藏与其他客户端应用程序关联的所有操作。  
  
 **Description**  
 键入操作说明（可选）。  
  
 **Caption**  
 当“标题是 MDX”设置为 **False** 时，在客户端应用程序中键入要为操作显示的标题。  
  
 当“标题是 MDX”设置为 **True** 时，键入返回标题字符串的多维表达式 (MDX)。  
  
 **标题是 MDX**  
 选择 **False** 表示“标题”包含一个文字字符串，该字符串表示将在客户端应用程序中为该操作显示的标题。  
  
 选择 **True** 表示 **“标题”** 包含一个 MDX 表达式，该表达式返回一个表示将在客户端应用程序中为该操作显示的标题的字符串。 必须在将该操作返回给客户端应用程序之前解析 MDX 表达式。  
  
## <a name="see-also"></a>请参阅  
 [多维表达式&#40;MDX&#41;引用](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [操作&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [操作组织程序&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [计算工具&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [操作窗体编辑器&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [报表操作窗体编辑器&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
