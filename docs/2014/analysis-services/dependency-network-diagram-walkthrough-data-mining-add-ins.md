---
title: 依赖关系网络关系图演练 （数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db069b243a0d06c142651ab4dcadd68e1e06657f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081972"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>依赖关系网络关系图演练（数据挖掘外接程序）
  几种不同的数据挖掘模型将网络图用作探索数据中各种关系的方法。 可以将这些模型导入使用 Visio**依赖关系网络**形状，然后再继续进行自定义和增强布局。 **Visio 数据挖掘形状**包括以下自定义控件适用于依赖关系网络关系图：  
  
-   网络图的呈现控件  
  
     这些选项包括在将形状置于 Visio 工作区中时启动的向导中。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与依赖关系网络图交互。  
  
## <a name="build-a-dependency-network-graph"></a>生成依赖关系网络图  
 将形状置于 Visio 页上，以启动**依赖关系网络 Visio 形状向导**并设置关系图选项。  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>使用依赖关系网络 Visio 形状向导  
  
1.  如果没有看到**Microsoft 数据挖掘形状**中**形状**列表中，单击**更多形状**，选择**打开模具**，并打开默认安装位置中的模板。  
  
     \<驱动器 >: \Program 文件 (x85) \Microsoft SQL Server 2012 数据挖掘外接程序  
  
2.  拖动**依赖关系网络**形状拖到页面上以启动向导。 单击“下一步”  。  
  
3.  在欢迎页上**依赖关系网络 Visio 形状向导**，单击**下一步**。  
  
4.  上**选择数据源**页**依赖关系网络 Visio 形状向导**，选择连接到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]待显示模型所在的服务器。  
  
5.  选择相应的挖掘模型，然后单击**下一步**。  
  
     若要选择适当的模型，可以查看名称、 说明、 列和中的数据类型**属性**窗格。  
  
     此形状支持通过使用以下算法创建的模型：  
  
    -   Naïve Bayes  
  
    -   决策树  
  
    -   关联规则  
  
6.  在页上，**选择呈现的节点**、 自定义的关系图的大小和 （可选） 筛选以仅包括某些节点。  
  
     大型数据集，依赖项关系图可以变得很大，并且都包含许多相关的对象，表示为*节点*。 通过使用此对话框，可以创建仅包含相关节点的自定义网络图。  
  
     [图形占位符]  
  
     **要提取的节点数**  
     如果该模型包含的节点数少于指定的节点数，则此设置无效。 如果该模型包含的节点数多于指定的节点数，则仅显示最强节点。  
  
     **名称包含**  
     将此框留空然后单击绿色箭头，可检索该模型中的所有节点。  
  
     或者，键入一个字符串并单击绿色箭头，仅返回包含指定字符串的节点。  
  
     可使用示例数据创建的大多数模型都不是很大，因此对于本示例，请将节点数增加到 10，然后单击绿色箭头以运行查询并获取所有节点的列表。  
  
7.  单击**高级**设置图形的明暗度和形状选项。  
  
8.  单击**关闭**退出**高级**选项对话框，然后单击**完成**创建关系图。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 在 Visio 创建网络依赖关系图之后，可使用 Visio 中的功能继续修改和增强图形。  
  
 下图显示依赖关系网络图的默认布局。  
  
 [图形占位符]  
  
1.  使用**平移和缩放**控件，在**任务窗格**区域中的 Visio**视图**功能区中，若要专注于关系图的部分和关系图中移动。  
  
2.  使用不同的图形布局通过 Visio**重新布局页面**选项。  
  
3.  单击**外接程序**功能区，然后显示用来处理数据挖掘关系图的自定义工具栏之一：  
  
     **布局**  
     优化页面上节点的布局，更改视图，以便所有节点都可见。  
  
     **调整页大小**  
     更改页面的大小，以便所有节点都可见。  
  
     **边缘强度**  
     切换整个图形的边缘强度的显示。 边缘是节点间的连接。 您可以使用滑块控件筛选掉弱连接。  
  
     **滑块**  
     **滑块**有助于你控制的依赖关系网络关系图中显示的关系的强度。  
  
     该图形中的每个节点都代表一个状态。 箭头代表两个状态之间的转换以及与该转换相关联的概率。 若要减少该图形中的节点数量，可向上移动滑动条。  
  
     若要增加该图形中的节点数量，可向下移动滑动条。  
  
     **添加项**  
     此时将打开**选择呈现的节点**对话框中，以便你可以选择要添加到关系图的新节点。  
  
4.  您可根据需要使图形变得简单或详细并添加批注，同时保持与模型的连接。  
  
     [图形占位符]  
  
> [!WARNING]  
>  在 Office 2013 中，无法突出显示早期版本外接程序中提供的依赖节点和其他快捷菜单选项。  
  
## <a name="see-also"></a>请参阅  
 [解决 Visio 数据挖掘关系图问题&#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
