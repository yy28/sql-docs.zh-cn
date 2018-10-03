---
title: 操作窗体编辑器 （操作选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32d1389fcb780fab6a370e6a9043600461baec4b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225547"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>操作窗体编辑器（“操作”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“操作”** 选项卡上的“操作窗体编辑器”窗格创建和修改标准操作。  
  
## <a name="options"></a>选项  
 **名称**  
 键入操作的名称。  
  
 **操作目标**  
 展开可查看“目标类型”和“目标对象”选项。  
  
 **目标类型**  
 选择要与该操作关联的对象的类型。 服务器只向客户端返回适用于指定类型的对象的操作。 如果满足 **“条件”** ，并且选择了下表中指定的对象，则客户端可使用该操作。  
  
|ReplTest1|所选对象|  
|-----------|---------------------|  
|属性成员|从 **“目标对象”** 中的属性所处的级别中选择成员。|  
|单元|**“目标对象”** 中的命名集处于选中状态。 选择 **“所有单元”** 可以选择多维数据集中的所有单元。|  
|多维数据集|**“目标对象”** 中的多维数据集处于选中状态。 选择 CURRENTCUBE 可以使用当前多维数据集。<br /><br /> 注意：在可能会重命名多维数据集或将该操作复制到其他多维数据集时，使用 CURRENTCUBE 更为方便。 建议您使用 CURRENTCUBE 表示当前多维数据集。|  
|维度成员|**“目标对象”** 中维度的成员处于选中状态。|  
|层次结构|**“目标对象”** 中的层次结构处于选中状态。|  
|层次结构成员|**“目标对象”** 中层次结构的成员处于选中状态。|  
|级别|**“目标对象”** 中的级别处于选中状态。|  
|级别成员|**“目标对象”** 中级别的成员处于选中状态。|  
  
 **目标对象**  
 选择要与该操作关联的对象。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例仅将应用于所选对象的操作返回到客户端。 可用对象列表受所选 **“目标类型”** 的约束。  
  
 **条件(可选)**  
 输入描述可选条件（与“目标对象”一起使用）的多维表达式 (MDX) 表达式，以进一步限制该操作可用的时间。 表达式必须返回一个布尔值，如果为 True，指示该操作可用。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **操作内容**  
 展开此项可以查看“类型”和“操作表达式”选项。  
  
 **类型**  
 选择在运行操作时要执行的操作类型。 可用的操作类型包括：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|数据集|返回将由客户端应用程序运行和显示的表示多维数据集的多维表达式 (MDX) 语句。|  
|专有|对于此操作的 **“应用程序”** 设置所关联的客户端应用程序，返回该程序能够解释的专有字符串。|  
|行集|返回将由客户端应用程序运行和显示的表示表格格式行集的多维表达式 (MDX) 语句。|  
|。|返回将由客户端应用程序运行的命令字符串。|  
|URL|返回将由客户端应用程序通常使用 Internet 浏览器打开的统一资源定位器 (URL) 字符串。|  
  
 有关操作类型的详细信息，请参阅[操作（Analysis Services - 多维数据）](multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 **操作表达式**  
 键入用于将操作所返回的字符串返回到客户端应用程序进行执行的多维表达式 (MDX) 表达式。  
  
 **附加属性**  
 展开可查看“调用”、“应用程序”、“说明”、“标题”和“标题是 MDX”选项。,   
  
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
 键入可以解释“操作表达式”所返回字符串的应用程序的名称。  
  
 还可以使用此选项来标识最常使用此操作的客户端应用程序，并在弹出菜单中该操作的旁边显示相应的图标。  
  
> [!NOTE]  
>  此选项只是向客户端应用程序提供使用哪一个客户端应用程序执行某项操作的建议，并不直接控制对该操作的访问。 客户端应用程序将隐藏与其他客户端应用程序关联的所有操作。  
  
 **Description**  
 键入操作说明（可选）。  
  
 **Caption**  
 当“标题是 MDX”设置为 **False** 时，在客户端应用程序中键入要为操作显示的标题。  
  
 当“标题是 MDX”设置为 **True** 时，键入返回标题字符串的多维表达式 (MDX)。  
  
 **True**  
 选择 **False** 表示“标题”包含一个文字字符串，该字符串表示将在客户端应用程序中为该操作显示的标题。  
  
 选择 **True** 表示 **“标题”** 包含一个 MDX 表达式，该表达式返回一个表示将在客户端应用程序中为该操作显示的标题的字符串。 必须在将该操作返回给客户端应用程序之前解析 MDX 表达式。  
  
## <a name="see-also"></a>请参阅  
 [操作&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [操作组织程序&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [计算工具&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [钻取操作窗体编辑器&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [报表操作窗体编辑器&#40;操作选项卡，多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
