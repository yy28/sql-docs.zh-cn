---
title: "将 MicrosoftML 包与 SQL Server R Services 配合使用 | Microsoft Docs"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 705d56003364f7fecc45efb24094651d6c963cc8
ms.lasthandoff: 04/11/2017

---
# <a name="using-the-microsoftml-package-with-sql-server-r-services"></a>将 MicrosoftML 包与 SQL Server R Services 配合使用
Microsoft R Server 和 SQL Server vNext CTP 1.0 随附提供的 [**MicrosoftML**](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) 包包括 Microsoft 开发的多种机器学习算法，支持多核处理和快速数据流处理。 该包还包括文本处理和特征化的转换。

### <a name="new-machine-learning-algorithms"></a>新的机器学习算法


-  **快速线性。** 线性学习器基于可用于二元分类或回归的随机双坐标上升。 此模型支持 L1 和 L2 正则化。

- **快速树。** 这是一种提升决策树算法，最初称为“FastRank”，专为必应而开发。 它是最快速和最流行的学习器之一。 支持二元分类和回归。

- **快速林。** 根据随机林方法创建逻辑回归模型。 它相当于 RevoScaleR 中的 `rxLogit` 函数，但支持 L1 和 L2 正则化。 支持二元分类和回归。

- **逻辑回归。** 逻辑回归模型类似于 RevoScaleR 中的 `rxLogit` 函数，添加了对 L1 和 L2 正则化的支持。 支持二元或多类分类。

- **神经网络。** 神经网络模型可用于二元分类、多类分类和回归。 使用单个 GPU 支持可自定义的复杂网络和 GPU 加速。

- **单类 SVM。** 异常检测模型基于可用于不均衡数据集中二元分类的 SVM 方法。

## <a name="transformation-functions"></a>转换函数

**MicrosoftML** 包还包括以下可用于转换数据和提取功能的函数。

- `featurizeText()`
 
  在给定的文本字符串中生成 ngrams 数。 

  函数的选项包括：检测所用的语言、执行文本词汇切分和规范化、删除非索引字以及从文本生成功能。 

- `categorical()`

  生成类别字典并将每个类别转换为指示器向量。 
 
- `categoricalHash()`

  通过将值哈希化并将哈希值用作包中索引，将分类值转换为指示器数组。  

- `selectFeatures()` 

  通过对非默认值进行计数，或根据标签计算交互信息评分，从给定变量中选择功能子集。 

若要深入了解这些新功能，请参阅 [MicrosoftML functions](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)（MicrosoftML 函数）。

## <a name="support-for-microsoftml-in-r-services"></a>支持 R Services 中的 MicrosoftML

**MicrosoftML** 包与用于 **RevoScaleR** 包的数据处理管理完全集成。 目前，可以在任何基于 Windows 的计算上下文中使用 **MicrosoftML** 包，包括 SQL Server R Services。



## <a name="see-also"></a>另请参阅

[MicrosoftML 简介](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction)

[RevoScaleR 函数参考](https://msdn.microsoft.com/microsoft-r/scaler/scaler)



