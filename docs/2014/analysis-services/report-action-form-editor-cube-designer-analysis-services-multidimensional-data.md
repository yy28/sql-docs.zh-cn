---
title: 报表操作窗体编辑器（"操作" 选项卡，多维数据集设计器）（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eeb3df670097c0d511a9f5b779b6705f40a5e897
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070298"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>报表操作窗体编辑器（“操作”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“操作”** 选项卡上的 **“报表操作窗体编辑器”** 窗格，修改在 **“操作组织程序”** 窗格中选择的报表操作。  
  
## <a name="options"></a>选项  
 **名称**  
 键入操作的名称。  
  
 **操作目标**  
 展开可查看“目标类型”和“目标对象”选项。********  
  
 **目标类型**  
 选择要与该操作关联的对象的类型。 服务器只向客户端返回适用于指定类型的对象的操作。 如果满足 **“条件”** ，并且选择了下表中指定的对象，则客户端可使用该操作。  
  
|值|所选对象|  
|-----------|---------------------|  
|属性成员|从 **“目标对象”** 中的属性所处的级别中选择成员。<br /><br /> 注意：使用所选属性的其他用户层次结构将继承报表操作。|  
|单元|
  **“目标对象”** 中的命名集处于选中状态。 选择 **“所有单元”** 可以选择多维数据集中的所有单元。|  
|Cube|
  **“目标对象”** 中的多维数据集处于选中状态。 选择 CURRENTCUBE 可以使用当前多维数据集。<br /><br /> 注意：在可能会重命名多维数据集或将该操作复制到其他多维数据集时，使用 CURRENTCUBE 更为方便。 建议您使用 CURRENTCUBE 表示当前多维数据集。|  
|维度成员|
  **“目标对象”** 中维度的成员处于选中状态。|  
|层次结构|
  **“目标对象”** 中的层次结构处于选中状态。|  
|层次结构成员|
  **“目标对象”** 中层次结构的成员处于选中状态。|  
|级别|
  **“目标对象”** 中的级别处于选中状态。|  
|级别成员|
  **“目标对象”** 中级别的成员处于选中状态。|  
  
 **目标对象**  
 选择要与该操作关联的对象。 [!INCLUDE[msCoName](../includes/msconame-md.md)]将应用于所选对象的操作返回到客户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]端。 可用对象列表受所选 **“目标类型”** 的约束。  
  
 **条件(可选)**  
 输入描述可选条件（与“目标对象”一起使用）的多维表达式 (MDX) 表达式，以进一步限制该操作可用的时间。**** 表达式必须返回一个布尔值，如果为 True，指示该操作可用。  
  
 将所选元素从 **“计算工具”** 窗格拖至此选项中，可包含所选元素的 MDX 语法。  
  
 **报表服务器**  
 展开该选项可以查看“服务器名称”、“服务器路径”和“报表格式”选项。************  
  
 **服务器名称**  
 键入操作在其上[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]运行报表的实例的名称。  
  
 **服务器路径**  
 键入 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 实例上的报表的路径。 例如，键入 **Sales/YearlySalesByCategory**。  
  
 **报表格式**  
 选择返回报表时所采用的格式。 下表对可用的格式进行了说明：  
  
|值|说明|  
|-----------|-----------------|  
|HTML5|报表以 HTML 5.0 标准格式返回。|  
|HTML3|报表以 HTML 3.2 标准格式返回。|  
|Excel|报表以 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 工作簿 (.xls) 文件的形式返回。|  
|PDF|报表以 Adobe 可移植文档格式 (.pdf) 文件的形式返回。|  
  
 **参数(可选)**  
 展开该选项可以查看一个网格，在该网格中，可以为“报表”中指定的报表提供报表参数。**** 该网格包含以下列：  
  
|列|说明|  
|------------|-----------------|  
|**参数名称**|键入要传递给报表的报表参数名称。|  
|**参数值**|键入要传递给报表的报表参数值。<br /><br /> 单击省略号按钮 (**...**) 可以显示“MDX 生成器”对话框，并创建提供报表参数值的 MDX 表达式。**** 有关****“MDX 生成器”对话框的详细信息，请参阅[“MDX 生成器”（Analysis Services - 多维数据）](mdx-builder-analysis-services-multidimensional-data.md)。<br /><br /> 如果将参数设置为 MDX 表达式，在运行操作时将计算该表达式，否则将参数不做任何修改直接传递给报表。|  
  
 **其他属性**  
 展开可查看“调用”、“应用程序”、“说明”、“标题”和“标题是 MDX”选项。****, ****************  
  
 **调用**  
 选择相应设置，指示何时执行该操作。  
  
> [!NOTE]  
>  此选项只是向客户端应用程序提供何时执行某项操作的建议，并不直接控制对该操作的调用。  
  
 下表对可用的设置进行了说明：  
  
|值|说明|  
|-----------|-----------------|  
|Batch|操作应作为批处理操作或[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]任务的一部分运行。|  
|交互|在用户调用该操作时运行。|  
|处于打开状态|第一次打开多维数据集时运行该操作。|  
  
 **Application**  
 键入可以解释“操作表达式”所返回字符串的应用程序的名称。****  
  
 还可以使用此选项来标识最常使用此操作的客户端应用程序，并在弹出菜单中该操作的旁边显示相应的图标。  
  
> [!NOTE]  
>  此选项只是向客户端应用程序提供使用哪一个客户端应用程序执行某项操作的建议，并不直接控制对该操作的访问。 客户端应用程序将隐藏与其他客户端应用程序关联的所有操作。  
  
 **说明**  
 键入操作说明（可选）。  
  
 **Caption**  
 当****“标题是 MDX”设置为 **False** 时，在客户端应用程序中键入要为操作显示的标题。  
  
 当 **“标题是 MDX”** 设置为 **True**时，显示返回标题字符串的键入多维表达式 (MDX)。  
  
 **True**  
 选择 **False** 表示“标题”包含一个文字字符串，该字符串表示将在客户端应用程序中为该操作显示的标题。****  
  
 选择 **True** 表示 **“标题”** 包含一个 MDX 表达式，该表达式返回一个表示将在客户端应用程序中为该操作显示的标题的字符串。 必须在将该操作返回给客户端应用程序之前解析 MDX 表达式。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据集设计器&#41; &#40;Analysis Services 多维数据的操作&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具栏 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [操作管理器 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [计算工具 &#40;操作 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [操作窗体编辑器 &#40;"操作" 选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [钻取操作窗体编辑器 &#40;操作 "选项卡，多维数据集设计器&#41; &#40;Analysis Services 多维数据&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
