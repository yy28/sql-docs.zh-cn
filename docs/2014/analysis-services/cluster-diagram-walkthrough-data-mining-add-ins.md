---
title: 分类关系图演练 （数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: ee4a7a09471078753589463c058ba5ea2e39c4d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680913"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>分类关系图演练（数据挖掘外接程序）
  创建聚类分析模型后，可以将其导入使用 Visio**群集**形状，然后再继续进行自定义和增强布局。 **Visio 数据挖掘形状**包括以下适用于数据挖掘关系图的自定义控件：  
  
-   分类关系图的呈现控件  
  
     这些选项包括在**群集向导**形状置于 Visio 工作区中时启动。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与数据挖掘形状交互。 根据所用挖掘模型的类型，选项可能有所不同。  
  
## <a name="build-a-cluster-diagram"></a>生成分类关系图  
 本演练演示如何在 Visio 中生成和自定义分类关系图。  
  
 要按照演练内容操作，您应有一个可用分类模型。 如果还没有一个模型，使用[群集向导&#40;数据挖掘的 Excel 外接程序&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)向导并创建在示例工作簿，使用所有默认值中使用的训练数据集的模型。  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>使用分类 Visio 形状向导  
  
1.  如果没有看到**Microsoft 数据挖掘形状**中**形状**列表中，单击**更多形状**，选择**打开模具**，并打开默认安装位置中的模板。  
  
     \<驱动器 >: files\microsoft SQL Server 2012 DM Add-ins  
  
2.  拖动**群集**形状拖到页。  
  
3.  在欢迎页上**分类 Visio 形状向导**，单击**下一步**。  
  
4.  上**选择数据源**页**群集向导**，选择连接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]要实现可视化效果包含数据挖掘模型的服务器。  
  
5.  选择相应的挖掘模型，然后单击**下一步**。  
  
     若要确保你选择了聚类分析模型，请查看中的说明**属性**窗格。  
  
6.  如果连接成功，请在页上，**分类关系图选项**，您决定哪种类型的分类关系图以 Visio 演示文稿中包括：  
  
     **仅显示分类形状**  
     此选项会创建一个简单的分类关系图，每个分类用一个矩形或您选择的其他形状表示。  
  
     **用特征图显示分类**  
     此选项会创建与上面相同的图表，但形状内是描述分类特征的直方图。  
  
     ![在 Visio 中群集特征图的示例](media/dm13-visio-cluster-samplecharshape.gif "在 Visio 中群集特征图的示例")  
  
     **用对比图显示分类**  
     此选项会创建与分类关系图相同的图表，但它会列出将当前分类与其他分类区分开来的最明显的特征。  
  
     在向导生成关系图后，您可以切换到其他图表类型，具体方法是右键单击某一分类并选择一种新的图表类型。 现在，选择选项，**用特征图显示分类**。  
  
7.  保留选项**图表中的行数**，为 5。  
  
     此选项不会更改模型; 中的分类的数它只是限制可以为每个分类的特征显示的属性的数目。  
  
     但是，此选项用作图表数据筛选器使您不能增加项目数。  
  
8.  单击 **“高级”**。  
  
     **群集选项**对话框中，您可以自定义关系图中使用的形状的可视外观。 您可以更改图形中使用的颜色和用于分类的形状。  
  
     **明暗度变量**控件不能在 Office 2013 中。  
  
     ![单击高级以选择形状颜色](media/dm13-visio-clusteroptions-advanced.gif "单击高级以选择形状颜色")  
  
     **提示：** 可以使用 Visio 主题和形状编辑控件更高版本更改某些颜色。 但是，Visio 主题还会覆盖这些颜色选择中的一部分，因此我们建议您从默认颜色开始，逐步应用更改。  
  
9. 单击**完成**创建关系图。  
  
     向导将从数据挖掘模型中检索信息、呈现形状并使用属性和值填充每个分类。  
  
     ![依赖关系网络](media/dm13-visiodepnet-defaultgraph.gif "依赖关系网络")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 完成关系图后，您可以继续使用 Visio 控件自定义外观，如下面示例所示。  
  
 ![使用 Visio 自定义的分类关系图](media/dm13-visio-clustercomplete1.gif "使用 Visio 自定义的分类关系图")  
  
 所有基本分类形状都由向导生成；使用以下工具可以对关系图进行升级和个性化设置：  
  
1.  拖动滑块**群集选项**控件，用来筛选出较弱的关系，并简化关系图。  
  
2.  使用 Visio**重新布局页面**选项可以使用不同的群集布局。  
  
3.  使用**连接器**选项卡上**设计**选项卡以更改连接器样式，使线条与分类不交叉。  
  
4.  单击**外接程序**功能区，然后显示用来处理数据挖掘关系图的自定义工具栏之一：  
  
     **布局**  
     优化分类的排列以适合当前页。  
  
     **调整页大小**  
     此控件适用于早期 HTML 版本。 请改用 Visio 页面大小调整控件。  
  
     **说明**  
     选择一个分类后，单击此选项可显示有关该分类的详细信息。  
  
     ![单击说明以获取有关群集的详细信息](media/dm13-visio-cluster-description-control.gif "单击说明以获取有关群集的详细信息")  
  
     **边缘强度**  
     在连接分类的线条上显示置信度得分。  
  
     但是，如果您使用任意特殊格式而不是向导默认生成的格式，包括一些背景，这些数字可能不会显示。  
  
     **滑块**  
     筛选分类之间的线条。 向上移动滑块会删除最重要关联外的所有关联。  
  
     **明暗度**  
     此控件在 Office 2013 中不能使用。  
  
5.  使用**平移和缩放**控件，在**任务窗格**区域中的 Visio**视图**功能区，以专注于一组群集和关系图中移动。  
  
6.  右键单击任意分类可查看分类形状的特定选项：  
  
    -   更改图表样式。  
  
    -   添加分类特征图。  
  
    -   添加分类对比图。  
  
## <a name="see-also"></a>请参阅  
 [解决 Visio 数据挖掘关系图问题&#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
