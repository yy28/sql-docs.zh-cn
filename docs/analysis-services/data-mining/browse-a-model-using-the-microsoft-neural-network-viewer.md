---
title: 使用 Microsoft 神经网络查看器浏览模型 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 280e8fa3702868ff36c799443b87b0827a962a89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676089"
---
# <a name="browse-a-model-using-the-microsoft-neural-network-viewer"></a>使用 Microsoft 神经网络查看器浏览模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
   [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 神经网络查看器显示使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法生成的挖掘模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络算法创建可分析多个输入和输出的分类和回归挖掘模型，它对于开放的分析和浏览十分有用。 有关此算法的详细信息，请参阅 [Microsoft Neural Network Algorithm](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)。  
  
 在您使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络查看器浏览某一模型时，通常会选择某个目标属性和状态，然后使用该查看器来查看输入属性是如何影响结果的。  
  
 例如，假设您知道与某一类别的潜在客户相关的以下事实：  
  
-   中年人（40 至 50 岁）。  
  
-   拥有一套住房。  
  
-   有两个孩子仍住在家中。  
  
 如何将这些属性与客户将进行购买的可能性相关联？  
  
 通过将购买行为用作目标结果来生成一个神经网络模型，您可以浏览针对客户属性（例如高收入）的多个组合，并且发现哪一属性组合最有可能影响购买行为。 例如，您可能会发现决定因素是到工作单位的距离。  
  
 如果您需要更详细的视图信息，例如表示已发现的每个模式的方程式，则可以切换视图并且使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
##  <a name="BKMK_ViewerTabs"></a> 查看器的选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 神经网络查看器提供以下用于浏览神经网络挖掘模型的选项卡：  
  
-   [输入](#BKMK_Inputs)  
  
-   [输出](#BKMK_Outputs)  
  
-   [变量](#BKMK_Characteristics)  
  
###  <a name="BKMK_Inputs"></a> 输入  
 使用 **“输入”** 选项卡可以选择模型用作输入的属性及属性值。 该查看器打开时，默认设置是包含所有属性。 在此默认视图中，模型将选择哪些属性值是要显示的最重要的属性值。  
  
 若要选择输入属性，请在“输入”网格的“属性”列内部单击，再从下拉列表中选择一个属性。 （该列表中只包含在该模型中包含的属性。）  
  
 第一个非重复值出现在 **“值”** 列下。 单击默认值将显示一个包含关联属性的所有可能状态的列表。 可以选择要调查的状态。 可以根据需要选择多个属性。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Outputs"></a> 输出  
 使用 **“输出”** 选项卡可以选择要调查的结果属性。 您可以选择任何两个结果状态来进行比较，并且假定在创建模型时列已定义为可预测属性。  
  
 使用 **OutputAttribute** 列表选择一个属性。 然后，可以从 **“值 1”** 和 **“值 2”** 列表中选择两个与该属性关联的状态。 输出属性的这两个状态将在 **“变量”** 窗格中进行比较。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 变量  
 中的网格**变量**选项卡包含以下各列：**特性**，**值**， **Favors [value 1]**，并且**Favors [value 2]**。 默认情况下，这些列按“Favors [value 1]”强度进行排序。 单击列标题将更改所选列的排序顺序。  
  
 属性右侧的条表示指定输入属性状态所倾向的输出属性状态。 条的大小则表示输出状态倾向于输入状态的程度。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Neural Network Algorithm](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [挖掘模型查看器任务和操作指南](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [数据挖掘模型查看器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
