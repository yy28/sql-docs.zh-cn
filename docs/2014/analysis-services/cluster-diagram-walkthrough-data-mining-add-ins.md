---
title: 分类关系图演练（数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc2df250b0728934f258c8217d29adfb91e66ff5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087904"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>分类关系图演练（数据挖掘外接程序）
  创建了聚类分析模型之后，可以使用 "**分类**" 形状将其导入 Visio，然后继续自定义并增强布局。 **Visio 数据挖掘形状**包含以下用于处理数据挖掘关系图的自定义控件：  
  
-   分类关系图的呈现控件  
  
     这些选项是在将形状拖放到 Visio 工作区中时启动的 "**群集向导**" 的一部分。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与数据挖掘形状交互。 根据所用挖掘模型的类型，选项可能有所不同。  
  
## <a name="build-a-cluster-diagram"></a>生成分类关系图  
 本演练演示如何在 Visio 中生成和自定义分类关系图。  
  
 要按照演练内容操作，您应有一个可用分类模型。 如果没有模型，请使用[群集向导 &#40;Excel 的数据挖掘外接程序 "&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)向导，并使用示例工作簿中的定型数据集创建一个模型，并使用所有默认值。  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>使用分类 Visio 形状向导  
  
1.  如果在 "**形状**" 列表中看不到 " **Microsoft 数据挖掘形状**"，请单击 "**更多形状**"，选择 "**打开模具**"，然后从默认安装位置打开模板。  
  
     \<驱动器>： \Program files\Microsoft SQL Server 2012 DM 外接程序  
  
2.  将**群集**形状拖到页面上。  
  
3.  在**群集 Visio 形状向导**的 "欢迎" 页上，单击 "**下一步**"。  
  
4.  在**群集向导**的 " [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] **选择数据源**" 页上，选择一个与服务器的连接，该服务器包含要显示的数据挖掘模型。  
  
5.  选择适当的挖掘模型，然后单击 "**下一步**"。  
  
     若要确保选择聚类分析模型，请在 "**属性**" 窗格中查看说明。  
  
6.  如果连接成功，则在 "**分类关系图" 选项**的 "选项" 中，确定要包括在 Visio 演示中的分类关系图类型：  
  
     **仅显示分类形状**  
     此选项会创建一个简单的分类关系图，每个分类用一个矩形或您选择的其他形状表示。  
  
     **用特征图显示分类**  
     此选项会创建与上面相同的图表，但形状内是描述分类特征的直方图。  
  
     ![Visio 中群集特征图的示例](media/dm13-visio-cluster-samplecharshape.gif "Visio 中群集特征图的示例")  
  
     **用对比图显示分类**  
     此选项会创建与分类关系图相同的图表，但它会列出将当前分类与其他分类区分开来的最明显的特征。  
  
     在向导生成关系图后，您可以切换到其他图表类型，具体方法是右键单击某一分类并选择一种新的图表类型。 现在，选择选项 "**显示具有特征的分类" 图表**。  
  
7.  保留该选项，**图表中的行数**为5。  
  
     此选项不会更改模型中的分类数;它只是限制可显示为每个分类的功能的属性数。  
  
     但是，此选项将作为图表数据的筛选器，因此不能再增加项的数量。  
  
8.  单击“高级”。   
  
     在 "**群集选项**" 对话框中，您可以自定义在关系图中使用的形状的可视外观。 您可以更改图形中使用的颜色和用于分类的形状。  
  
     "**明暗度变量**" 控件在 Office 2013 中不起作用。  
  
     ![单击“高级”以选择形状颜色](media/dm13-visio-clusteroptions-advanced.gif "单击“高级”以选择形状颜色")  
  
     **提示：** 稍后，可以使用 Visio 主题和形状编辑控件更改某些颜色。 但是，Visio 主题还会覆盖这些颜色选择中的一部分，因此我们建议您从默认颜色开始，逐步应用更改。  
  
9. 单击 "**完成**" 以创建关系图。  
  
     向导将从数据挖掘模型中检索信息、呈现形状并使用属性和值填充每个分类。  
  
     ![依赖关系网络](media/dm13-visiodepnet-defaultgraph.gif "依赖关系网络")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 完成关系图后，您可以继续使用 Visio 控件自定义外观，如下面示例所示。  
  
 ![使用 Visio 自定义的群集关系图](media/dm13-visio-clustercomplete1.gif "使用 Visio 自定义的群集关系图")  
  
 所有基本分类形状都由向导生成；使用以下工具可以对关系图进行升级和个性化设置：  
  
1.  拖动 "**群集选项**" 控件中的滑块，筛选出较弱的关系并简化关系图。  
  
2.  使用 Visio "**重新布局页面**" 选项试验不同的群集布局。  
  
3.  使用 "**设计**" 选项卡上的 "**连接器**" 选项可以更改连接线样式，使线条不跨越分类。  
  
4.  单击 "**外接程序**" 功能区，然后显示用于处理数据挖掘关系图的自定义工具栏之一：  
  
     **布局**  
     优化分类的排列以适合当前页。  
  
     **调整页大小**  
     此控件适用于早期 HTML 版本。 请改用 Visio 页面大小调整控件。  
  
     **说明**  
     选择一个分类后，单击此选项可显示有关该分类的详细信息。  
  
     ![单击“说明”以获取有关该群集的详细信息](media/dm13-visio-cluster-description-control.gif "单击“说明”以获取有关该群集的详细信息")  
  
     **边缘强度**  
     在连接分类的线条上显示置信度得分。  
  
     但是，如果您使用任意特殊格式而不是向导默认生成的格式，包括一些背景，这些数字可能不会显示。  
  
     **滑块**  
     筛选分类之间的线条。 向上移动滑块会删除最重要关联外的所有关联。  
  
     **明暗度**  
     此控件在 Office 2013 中不能使用。  
  
5.  使用 Visio "**视图**" 功能区的 "**任务窗格**" 区域中的 "**平移和缩放**" 控件，可以重点关注一组分类并四处移动关系图。  
  
6.  右键单击任意分类可查看分类形状的特定选项：  
  
    -   更改图表样式。  
  
    -   添加分类特征图。  
  
    -   添加分类对比图。  
  
## <a name="see-also"></a>另请参阅  
 [解决 Visio 数据挖掘关系图 &#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
