---
title: 依赖关系网络关系图演练（数据挖掘外接程序） |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081972"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>依赖关系网络关系图演练（数据挖掘外接程序）
  几种不同的数据挖掘模型将网络图用作探索数据中各种关系的方法。 您可以使用 "**依赖关系网络**" 形状将这些模型导入 Visio，然后继续自定义并增强布局。 **Visio 数据挖掘形状**包含以下用于处理依赖关系网络关系图的自定义控件：  
  
-   网络图的呈现控件  
  
     这些选项包括在将形状置于 Visio 工作区中时启动的向导中。  
  
-   **数据挖掘布局**工具栏  
  
     这些选项将添加到 Visio 工作区以便与依赖关系网络图交互。  
  
## <a name="build-a-dependency-network-graph"></a>生成依赖关系网络图  
 您将形状拖放到 Visio 页面上，启动 "**依赖关系网络 Visio 形状向导**" 并设置关系图选项。  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>使用依赖关系网络 Visio 形状向导  
  
1.  如果在 "**形状**" 列表中看不到 " **Microsoft 数据挖掘形状**"，请单击 "**更多形状**"，选择 "**打开模具**"，然后从默认安装位置打开模板。  
  
     \<驱动器>： \Program files （x85） \Microsoft SQL Server 2012 DM 外接程序  
  
2.  将 "**依赖关系网络**" 形状拖到页面上以启动向导。 单击“下一步”  。  
  
3.  在 "**依赖关系网络 Visio 形状向导**" 的 "欢迎" 页上，单击 "**下一步**"。  
  
4.  在 "**依赖关系网络 Visio 形状向导**" 的 "**选择数据源**" 页上，选择与[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]要可视化的模型的服务器之间的连接。  
  
5.  选择适当的挖掘模型，然后单击 "**下一步**"。  
  
     若要选择适当的模型，可以在 "**属性**" 窗格中查看名称、说明、列和数据类型。  
  
     此形状支持通过使用以下算法创建的模型：  
  
    -   Naïve Bayes  
  
    -   决策树  
  
    -   关联规则  
  
6.  在页上，**选择要呈现的节点**，自定义关系图的大小，并根据需要进行筛选，以便只包含某些节点。  
  
     对于大型数据集，依赖关系图可能会变得很大，并且包含许多相关对象，这些对象表示为*节点*。 通过使用此对话框，可以创建仅包含相关节点的自定义网络图。  
  
     [艺术占位符]  
  
     **要提取的节点数**  
     如果该模型包含的节点数少于指定的节点数，则此设置无效。 如果该模型包含的节点数多于指定的节点数，则仅显示最强节点。  
  
     **名称包含**  
     将此框留空然后单击绿色箭头，可检索该模型中的所有节点。  
  
     或者，键入一个字符串并单击绿色箭头，仅返回包含指定字符串的节点。  
  
     可使用示例数据创建的大多数模型都不是很大，因此对于本示例，请将节点数增加到 10，然后单击绿色箭头以运行查询并获取所有节点的列表。  
  
7.  单击 "**高级**" 设置图形的明暗度和形状选项。  
  
8.  单击 "**关闭**" 以退出 "**高级**选项" 对话框，然后单击 "**完成**" 以创建关系图。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>浏览和修改已完成的关系图  
 在 Visio 创建网络依赖关系图之后，可使用 Visio 中的功能继续修改和增强图形。  
  
 下图显示依赖关系网络图的默认布局。  
  
 [艺术占位符]  
  
1.  使用 Visio "**视图**" 功能区的 "**任务窗格**" 区域中的 "**平移和缩放**" 控件，可以重点关注关系图的某个部分并四处移动关系图。  
  
2.  使用 Visio "**重新布局页面**" 选项提供的不同图形布局进行试验。  
  
3.  单击 "**外接程序**" 功能区，然后显示用于处理数据挖掘关系图的自定义工具栏之一：  
  
     **布局**  
     优化页面上节点的布局，更改视图，以便所有节点都可见。  
  
     **调整页大小**  
     更改页面的大小，以便所有节点都可见。  
  
     **边缘强度**  
     切换整个图形的边缘强度的显示。 边缘是节点间的连接。 您可以使用滑块控件筛选掉弱连接。  
  
     **Slider**  
     **滑块**可帮助控制依赖关系网络关系图中显示的关系的强度。  
  
     该图形中的每个节点都代表一个状态。 箭头代表两个状态之间的转换以及与该转换相关联的概率。 若要减少该图形中的节点数量，可向上移动滑动条。  
  
     若要增加该图形中的节点数量，可向下移动滑动条。  
  
     **添加项**  
     打开 "**选择要呈现的节点**" 对话框，以便您可以选择要添加到关系图中的新节点。  
  
4.  您可根据需要使图形变得简单或详细并添加批注，同时保持与模型的连接。  
  
     [图形占位符]  
  
> [!WARNING]  
>  在 Office 2013 中，无法突出显示早期版本外接程序中提供的依赖节点和其他快捷菜单选项。  
  
## <a name="see-also"></a>另请参阅  
 [解决 Visio 数据挖掘关系图 &#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
