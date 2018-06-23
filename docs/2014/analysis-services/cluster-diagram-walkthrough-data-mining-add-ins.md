---
title: 群集关系图演练 （数据挖掘外接程序） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a8ab399dcc59873cc507e260eec82582a69f8ba6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128892"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>分类关系图演练（数据挖掘外接程序）
  在创建聚类分析模型后，可以将其导入 Visio 使用**群集**形状，然后继续自定义和增强布局。 **Visio 数据挖掘形状**包括用于处理数据挖掘关系图的以下自定义控件：  
  
-   分类关系图的呈现控件  
  
     这些选项属于**群集向导**当形状放到 Visio 工作区时，将启动。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与数据挖掘形状交互。 根据所用挖掘模型的类型，选项可能有所不同。  
  
## <a name="build-a-cluster-diagram"></a>生成分类关系图  
 本演练演示如何在 Visio 中生成和自定义分类关系图。  
  
 要按照演练内容操作，您应有一个可用分类模型。 如果没有一个模型，使用[群集向导&#40;for Excel 的数据挖掘外接&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)向导并创建在示例工作簿，使用所有默认值中使用的训练数据集的模型。  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>使用群集 Visio 形状向导  
  
1.  如果看不到**Microsoft 数据挖掘形状**中**形状**列表中，单击**更多形状**，选择**打开模具**，并打开默认安装位置中的模板。  
  
     \<驱动器 >: files\microsoft SQL Server 2012 数据挖掘外接程序  
  
2.  拖动**群集**拖到页面上的形状。  
  
3.  在欢迎页上的**群集 Visio 形状向导**，单击**下一步**。  
  
4.  上**选择数据源**页**群集向导**，选择的连接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您要实现可视化包含的数据挖掘模型的服务器。  
  
5.  选择相应的挖掘模型，然后单击**下一步**。  
  
     若要确保你选择聚类分析模型，查看中的说明**属性**窗格。  
  
6.  如果连接成功，在页上，**分类关系图的选项**，您决定哪种类型的分类关系图，要包括在 Visio 演示文稿中：  
  
     **显示群集形状**  
     此选项会创建一个简单的分类关系图，每个分类用一个矩形或您选择的其他形状表示。  
  
     **用特征图显示群集**  
     此选项会创建与上面相同的图表，但形状内是描述分类特征的直方图。  
  
     ![在 Visio 中的群集特征图表的示例](media/dm13-visio-cluster-samplecharshape.gif "在 Visio 中的群集特征图表的示例")  
  
     **用对比图显示群集**  
     此选项会创建与分类关系图相同的图表，但它会列出将当前分类与其他分类区分开来的最明显的特征。  
  
     在向导生成关系图后，您可以切换到其他图表类型，具体方法是右键单击某一分类并选择一种新的图表类型。 现在，选择选项，**显示用特征图群集**。  
  
7.  清除该选项，**图表中的行数**，为 5。  
  
     此选项不会更改模型中的分类数；它只是限制可作为每种分类特征显示的属性数。  
  
     不过此选项用作图表数据筛选器，因此之后不能增加项目数。  
  
8.  单击 **“高级”**。  
  
     **群集选项**对话框中，你可以自定义关系图中所用形状的可视外观。 您可以更改图形中使用的颜色和用于分类的形状。  
  
     **明暗度变量**Office 2013 中，控件不起作用。  
  
     ![单击高级以选择形状颜色](media/dm13-visio-clusteroptions-advanced.gif "单击高级以选择形状颜色")  
  
     **提示：** 某些颜色更高版本可以更改通过使用 Visio 主题和编辑控件的形状。 但是，Visio 主题还会覆盖这些颜色选择中的一部分，因此我们建议您从默认颜色开始，逐步应用更改。  
  
9. 单击**完成**以创建关系图。  
  
     向导将从数据挖掘模型中检索信息、呈现形状并使用属性和值填充每个分类。  
  
     ![依赖关系网络](media/dm13-visiodepnet-defaultgraph.gif "依赖关系网络")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 完成关系图后，您可以继续使用 Visio 控件自定义外观，如下面示例所示。  
  
 ![使用 Visio 自定义的分类关系图](media/dm13-visio-clustercomplete1.gif "使用 Visio 自定义的分类关系图")  
  
 所有基本分类形状都由向导生成；使用以下工具可以对关系图进行升级和个性化设置：  
  
1.  将滑块拖动**群集选项**控制，用于以筛选出较弱的关系，并简化序列图。  
  
2.  使用 Visio**重新布局页**选项进行实验，以使用不同的群集布局。  
  
3.  使用**连接器**选项**设计**选项卡以更改要与交叉群集保留行的连接器样式。  
  
4.  单击**外接程序**功能区，，然后显示一个自定义用于处理数据挖掘关系图的工具栏：  
  
     **布局**  
     优化分类的排列以适合当前页。  
  
     **调整页的大小**  
     此控件适用于早期 HTML 版本。 请改用 Visio 页面大小调整控件。  
  
     **Description**  
     选择一个分类后，单击此选项可显示有关该分类的详细信息。  
  
     ![单击以获取有关群集的详细信息的说明](media/dm13-visio-cluster-description-control.gif "单击说明以获取有关群集的详细信息")  
  
     **边缘强度**  
     在连接分类的线条上显示置信度得分。  
  
     但是，如果您使用任意特殊格式而不是向导默认生成的格式，包括一些背景，这些数字可能不会显示。  
  
     **滑块**  
     筛选分类之间的线条。 向上移动滑块会删除最重要关联外的所有关联。  
  
     **明暗度**  
     此控件在 Office 2013 中不能使用。  
  
5.  使用**平移和缩放**控件在**任务窗格**Visio 区域**视图**功能区中，若要专注于一组群集和关系图中移动。  
  
6.  右键单击任意分类可查看分类形状的特定选项：  
  
    -   更改图表样式。  
  
    -   添加分类特征图。  
  
    -   添加分类对比图。  
  
## <a name="see-also"></a>请参阅  
 [Visio 数据挖掘关系图疑难解答&#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  