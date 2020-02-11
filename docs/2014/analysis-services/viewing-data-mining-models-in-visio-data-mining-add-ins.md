---
title: 在 Visio 中查看数据挖掘模型（数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c287e840c07d11a527e980f9f07fb39fb3852739
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065522"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>在 Visio 中查看数据挖掘模型（数据挖掘外接程序）
  通过 Visio 数据挖掘形状，您可以连接服务器并创建一个表示现有数据挖掘模型的关系图。 然后，可以使用 Visio 控件对关系图进行自定义，也可以深化到数据来公开一些基础统计信息并利用基础模型。  
  
## <a name="building-a-model-diagram"></a>生成模型关系图  
 打开包含用于数据挖掘的 Visio 形状的文件时，"**形状**" 窗格将显示以下形状。  
  
 如果在打开 Visio 时没有显示数据挖掘形状，则请从安装文件夹打开模板文件。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 若要使用形状，则请将其拖至该页。 每个形状都会打开一个不同的向导，可帮助您选择源数据，设置特定关系图类型的选项，以及指定明暗度和其他显示选项。  
  
 下表列出了可用于各关系图类型的模型类型。  
  
|Visio 形状|支持的模型|  
|-----------------|----------------------|  
|决策树|此形状用于基于决策树算法或线性回归算法的模型。|  
|依赖关系网络|此形状用于基于以下任何算法的模型：Naive Bayes、决策树或关联规则。|  
|群集|此形状用于基于聚类分析算法的模型。|  
  
 根据挖掘模型中的数据类型的不同，向导可能会具有不同的选项。 例如，包含连续数字的列和包含分类变量的列显示不同。  
  
## <a name="working-with-completed-shapes"></a>使用已完成的形状  
 完成关系图后，可以用它浏览数据挖掘模型或增强关系图以便在演示中使用。  
  
### <a name="visio-menus"></a>Visio 菜单  
 Visio 提供了多种呈现控件、主题和快捷菜单以帮助您增强关系图。  
  
-   使用 Visio 主题更改关系图颜色。  
  
-   更改连接器或图表布局。  
  
### <a name="data-mining-menus"></a>数据挖掘菜单  
 这些工具栏和菜单由每种形状和模型类型特定的外接程序提供。  
  
-   每个关系图类型都具有针对形状的快捷菜单，可用于访问特殊选项。 尽管此菜单中的许多选项都是所有 Visio 形状共有的，但某些选项对于数据挖掘模板是唯一的  
  
     例如，在决策树关系图中，您可单击单个节点然后折叠子节点以使关系图更简单，或者将子节点移到单独的页。  
  
-   由于形状绑定到模型数据，所以您也可以使用关系图进行一些浏览：  
  
     筛选显示的节点，或更改树的级别或图形深度。  
  
     放大特定部分、搜索包含某个属性的节点或者按其边缘（概率）筛选依赖关系图。  
  
## <a name="walkthroughs"></a>演练  
 有关如何使用和解释某一已完成关系图的示例，请参阅以下主题：  
  
 [分类关系图演练](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [依赖关系网络关系图演练](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [决策树关系图演练](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>另请参阅  
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
