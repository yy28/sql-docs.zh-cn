---
title: 决策树关系图演练（数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shapes, data mining
- diagram, decision tree
- Visio shapes, decision tree
- decision tree [data mining]
ms.assetid: 9566f6a2-c750-4125-ba5e-42c7251a78c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef951825144f381ab37a83526ec96321fe43cfec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082281"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>决策树关系图演练（数据挖掘外接程序）
  如果您已创建决策树模型，则可以使用决策树形状或依赖关系网络形状在 Visio 创建自定义关系图。 本主题介绍使用**决策树**形状和这些控件可以执行的自定义：  
  
-   决策树关系图的呈现控件  
  
     这些选项是在将形状拖放到 Visio 工作区中时启动的**决策树向导**的一部分。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与形状交互。  
  
## <a name="build-a-decision-tree-diagram"></a>生成决策树关系图  
 您将决策树形状拖到 Visio 页面上，以启动**决策树 Visio 形状向导**并设置关系图选项。  
  
#### <a name="use-the-decision-tree-wizard"></a>使用决策树向导  
  
1.  如果在 "**形状**" 列表中看不到 " **Microsoft 数据挖掘形状**"，请单击 "**更多形状**"，选择 "**打开模具**"，然后从默认安装位置打开模板。  
  
     \<驱动器>： \Program files （x85） \Microsoft SQL Server 2012 DM 外接程序  
  
2.  将**决策树**形状拖到页面上。  
  
3.  在**决策树 Visio 形状向导**的 "欢迎" 页上，单击 "**下一步**"。  
  
4.  在**群集向导**的 "**选择数据源**" 页上，选择与要可视化的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]模型的服务器之间的连接。  
  
5.  选择适当的挖掘模型，然后单击 "**下一步**"。  
  
     此关系图类型支持使用决策树或线性回归算法创建的模型。  
  
6.  在 "**选择决策树**" 页上，选择要显示的单个树。  
  
     树对导致已建模的特定结果的交互建模;因此，即使模型包含多个结果，一次只能显示一个树。  
  
7.  在 "**选择决策树**" 对话框中，您还可以设置这些呈现选项：  
  
     **最大呈现深度**  
     使用此选项可控制显示的节点数目。  
  
     决策树可能会变得很深，从而产生无法适合该页的关系图。 使用此控件可重点关注最左侧（也更加重要）的节点。  
  
     默认设置是三级节点。  
  
     **选择值的颜色和显示文本**  
     选择表示每种结果的颜色。 如果您不指定颜色，则会使用当前视频主题颜色自动生成颜色。  
  
8.  单击 "**高级**"，为决策树关系图中的每个节点自定义以下选项。  
  
     **明暗度变量**和**状态**  
     选择要在树关系图中显示的目标结果。  
  
     **显示直方图**  
     向每个节点添加图表以显示定义该节点的规则。  
  
     **显示标签**  
     向直方图添加列名称。  
  
     **显示概率**  
     显示每个值的概率。  
  
     **显示支持**  
     显示对每个值的支持。  
  
     **显示页脚**  
     添加用于将所有显示的值相加的页脚。  
  
     **显示页眉**  
     添加列标题。  
  
     **显示无支持的状态**  
     可用来显示缺失的值。  
  
9. 单击 "**完成**" 以创建关系图。  
  
    > [!WARNING]  
    >  在某些环境中，图表中的连接器可能无法在 Office 2013 中呈现。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 完成**决策树 Visio 形状向导**后，visio 会在页面上创建一个树关系图，以图形方式显示导致预测结果的规则。  
  
 您可以使用以下用于决策树关系图的控件继续修改形状。  
  
#### <a name="using-the-decision-tree-option-menus"></a>使用决策树选项菜单  
  
1.  单击 "**外接程序**" 功能区，然后显示用于处理数据挖掘关系图的自定义工具栏之一：  
  
     **布局**  
     优化树的排列以适合当前页。  
  
     **调整页大小**  
     此控件适用于早期 HTML 版本。 改用 Visio 页面大小调整控件。  
  
     **说明**  
     在选择树的一个节点后，单击此选项可显示有关该节点情况的详细信息。  
  
2.  使用 Visio 的 "**设计**" 功能区中的 "**重新布局页面**" 选项来试验不同的树布局。  
  
3.  使用 "**设计**" 选项卡上的 "**连接器**" 选项来更改在树中的节点之间使用的连接器。  
  
4.  使用 Visio "**视图**" 功能区的 "**任务窗格**" 区域中的 "**平移和缩放**" 控件，可以重点关注关系图的特定区域。  
  
5.  右键单击树中的任一节点，从与决策树关系图相关的以下快捷菜单选项中选择：  
  
     **优化页面布局**  
     在页面上平均分布节点，调整页面视图以便可以看到所有节点。  
  
     **将子级移到新页**  
     将当前所选节点的子级移到新页。  
  
     **折叠子节点**  
     隐藏当前所选节点的子级。  
  
     **展开子节点**  
     显示当前所选节点的子级。  
  
## <a name="see-also"></a>另请参阅  
 [解决 Visio 数据挖掘关系图 &#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
