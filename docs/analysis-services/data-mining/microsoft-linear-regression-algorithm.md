---
title: Microsoft 线性回归算法 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20d052ad91a00a7b70b658ff9118dfb73736a410
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183006"
---
# <a name="microsoft-linear-regression-algorithm"></a>Microsoft 线性回归算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法的一种变体，有助于计算依赖变量和独立变量之间的线性关系，然后使用该关系进行预测。  
  
 该关系采用的表示形式是最能代表数据序列的线的公式。 例如，以下关系图中的线是数据最可能的线性表示形式。  
  
 ![模型的一组数据的行](../../analysis-services/data-mining/media/linear-regression.gif "模型的一组数据的行")  
  
 关系图中的每个数据点都有一个与该数据点与回归线之间距离关联的错误。 回归方程式中的系数 a 和 b 可以调整回归线的角度和位置。 可以对 a 和 b 进行调整，直到与所有点都关联的错误总数达到最低值，以此获得回归公式。  
  
 还有其他类型的使用多个变量的线性回归以及非线性回归方法。 但是，线性回归是一种众所周知的有用方法，可对一些潜在因素中更改的响应进行建模。  
  
## <a name="example"></a>示例  
 可以使用线性回归确定两个连续列之间的关系。 例如，您可以使用线性回归根据生产或销售数据计算趋势线。 还可以使用线性回归作为基础，来开发更复杂的数据挖掘模型，以评估数据列之间的关系。  
  
 尽管有许多计算线性回归的方法，而且这些方法不需要数据挖掘工具，但是使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法计算线性回归的优势在于可以自动计算并测试变量之间所有可能的关系。 您不必选择计算方法，如计算最小平方法。 但对于结果受多个因素影响的应用场景，线性回归可能会过分简化其中的关系。  
  
## <a name="how-the-algorithm-works"></a>算法的原理  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法的一种变体。 如果选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法，将会调用带有参数的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法特例，这些参数不但会限定算法行为，而且还会要求输入数据的类型。 另外，在线性回归模型中，整个数据集都用于计算初始传递中的关系，而标准决策树模型则不断将数据拆分为更小的子集或树。  
  
## <a name="data-required-for-linear-regression-models"></a>线性回归模型所需的数据  
 在准备用于线性回归模型的数据时，应该了解特定算法的要求。 这包括所需数据量以及数据使用方式。 此模型类型的要求如下：  
  
-   **单键列** 每个模型都必须包含一个用于唯一标识每条记录的数值列或文本列。 不允许复合键。  
  
-   **可预测列** 至少需要一个可预测列。 可以在一个模型中包含多个可预测属性，但是这些可预测属性必须是连续数值数据类型。 不能将 datetime 数据类型用作可预测属性，即使数据的本机存储是数值类型。  
  
-   **输入列** ：输入列必须包含连续数值数据，并且向其分配相应的数据类型。  
  
 有关详细信息，请参阅 [Microsoft 线性回归算法技术参考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)。  
  
## <a name="viewing-a-linear-regression-model"></a>查看线性回归模型  
 若要浏览模型，可以使用 **“Microsoft 树查看器”** 。 线性回归模型的树结构非常简单，回归方程式的所有相关信息都包含在一个节点中。 有关详细信息，请参阅 [使用 Microsoft 树查看器浏览模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)。  
  
 如果想了解有关该方程式的更多详细信息，还可以使用 [“Microsoft 一般内容树查看器”](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)查看系数和其他详细信息。  
  
 对于线性回归模型，模型内容包括元数据、回归公式和有关输入值分布的统计信息。 有关详细信息，请参阅 [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
## <a name="creating-predictions"></a>创建预测  
 模型处理完毕后，结果将以一组统计信息和线性回归公式的形式存储，您可以利用这些结果来计算未来趋势。 有关用于线性回归模型的查询的示例，请参阅 [线性回归模型查询示例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)。  
  
 有关如何创建针对挖掘模型的查询的常规信息，请参阅 [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)。  
  
 除了通过选择 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法创建线性回归模型外，您还可以在可预测属性为连续数值数据类型时，创建包含回归的决策树模型。 在这种情况下，如果找到适当的分离点，该算法会对数据进行拆分；但对于某些数据区域，则会创建回归公式。 有关决策树模型中回归树的详细信息，请参阅[决策树模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
## <a name="remarks"></a>备注  
  
-   不支持使用预测模型标记语言 (PMML) 创建挖掘模型。  
  
-   不支持创建数据挖掘维度。  
  
-   支持钻取。  
  
-   支持使用 OLAP 挖掘模型。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘算法 &#40;Analysis Services-数据挖掘&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 线性回归算法技术参考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [线性回归模型查询示例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
