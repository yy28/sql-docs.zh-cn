---
title: 向结构中添加挖掘模型（Analysis Services 数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], creating
- mining models [Analysis Services], creating
- mining models [Analysis Services], modifying
ms.assetid: a175daa5-58ea-474c-a82f-9648c5155dc8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd25682f12ce0a3ddad5e8f135d82aaf08115762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086252"
---
# <a name="add-mining-models-to-a-structure-analysis-services---data-mining"></a>向结构中添加挖掘模型（Analysis Services - 数据挖掘）
  挖掘结构旨在支持多个挖掘模型。 因此，在完成向导后，您可以打开结构并添加新的挖掘模型。 每当您创建模型时，可以使用一个不同的算法、更改参数或应用筛选器，以使用不同的数据子集。  
  
## <a name="adding-new-mining-models"></a>添加新的挖掘模型  
 使用数据挖掘向导创建新的挖掘模型时，默认情况下，您必须总是先创建一个挖掘结构。 然后，该向导会为您提供用于向结构中添加初始挖掘模型的选项。 但是，不需要立即创建模型。 如果仅仅创建结构，则不需要决定将哪一列用作可预测的属性，或者如何在特定模型中使用这些数据。 您只需设置要在将来使用的通用数据结构，之后即可使用 [Data Mining Designer](data-mining-designer.md) 来添加基于此结构的新挖掘模型。  
  
> [!NOTE]  
>  在 DMX 中，CREATE MINING MODEL 语句以挖掘模型开头。 也就是说，您只需定义想要的挖掘模型， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会自动生成基础结构。 稍后，您可以使用 ALTER STRUCTURE ...，继续向该结构中添加新的挖掘模型。添加模型语句。  
  
## <a name="choosing-an-algorithm"></a>选择算法  
 当您向现有结构中添加新模型时，您首先应选择要在该模型中使用的数据挖掘算法。 选择算法很重要，因为每种算法都执行一种不同类型的分析并具有不同的要求。  
  
 当您选择了与您的数据不兼容的算法时，您将收到一个警告。 在某些情况下，您可能需要忽略该算法无法处理的列。 在其他情况下，该算法将自动进行调整以满足您需求。 例如，如果结构包含数值数据，并且算法仅适用于离散值，则算法会为您将数值组合到离散范围中。 在某些情况下，您可能需要先通过选择键或选择可预测属性来手动修复数据。  
  
 在创建新模型时无需更改算法。 通常，通过使用同一算法，但筛选数据或更改参数（例如，聚类分析方法或最小项集大小），可获得完全不同的结果。 建议您试用多个模型以查看可产生最佳结果的参数。  
  
 请注意，必须先处理所有新模型，然后才能使用这些模型。  
  
## <a name="specifying-the-usage-of-columns-in-a-new-mining-model"></a>指定新挖掘模型中的列用法  
 在向现有挖掘结构中添加新的挖掘模型时，必须指定该模型使用每个数据列的方式。 根据您为模型选择的算法类型，默认情况下，可能会做出其中一些选择。 如果没有指定列的使用类型，则挖掘结构中将不会包含该列。 但是，如果模型支持钻取功能，则该列中的数据仍可用于钻取。  
  
 模型所使用的挖掘结构中的列（如果未设置为“忽略”）必须是键、输入列、预测列或其值也用作模型的输入的预测列。  
  
-   键列包含表中每个行的唯一标识符。 某些挖掘模型（如基于顺序分析和聚类分析或者时序算法的挖掘模型）可能包含多个键列。 但是，这些键并非相关意义上的复合键，必须选择这些键才能为时序分析以及顺序分析和聚类分析提供支持。  
  
-   输入列提供据以进行预测的信息。 数据挖掘向导提供了 **“建议”** 功能，在选择预测列时将启用该功能。 如果您单击此按钮，则该向导将对可预测值进行采样并确定结构中生成变量的其他列。 它将拒绝键列或具有多个唯一值的其他列，并建议使用似乎与结果相关的列。  
  
     当数据集包含的列数多于生成挖掘模型所需的实际列数时，此功能特别有用。 
  **“建议”** 功能可以计算出一个数值分数（介于 0 到 1 之间），用于说明数据集中的每一列与预测列之间的关系。 根据此分数，该功能可以建议可用作挖掘模型的输入的列。 如果使用了 **“建议”** 功能，您就可以使用建议的列，修改选择的列以满足需要，也可以忽略建议。  
  
-   预测列包含要在挖掘模型中预测的信息。 可选择多个列作为可预测属性。 聚类分析模型属于例外情况，可预测属性在该模型中是可选的。  
  
     根据模型类型，可预测列可能必须为特定的数据类型：例如，线性回归模型需要数字列作为预测值；Naïve Bayes 算法需要离散值（并且所有输入也必须是离散的）。  
  
## <a name="specifying-column-content"></a>指定列内容  
 对于某些列，可能还需要指定“列内容” **。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘中，每个数据列的“内容类型”属性都通知算法应如何处理该列中的数据。 例如，如果数据包括一个“收入”列，则您必须通过将内容类型设置为“连续”来指定该列包含连续数。 但是，您还可以通过将内容类型设置为“离散化”并选择指定存储桶的准确数目，来指定“收入”列中的数分成存储桶。 您可以创建以不同方式处理列的不同模型：例如，您可能尝试使用一种模型将客户分成三个年龄组，而另一个模型则将客户分成 10 个年龄组。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构 &#40;Analysis Services 数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [创建关系挖掘结构](create-a-relational-mining-structure.md)   
 [挖掘模型属性](mining-model-properties.md)   
 [挖掘模型列](mining-model-columns.md)  
  
  
