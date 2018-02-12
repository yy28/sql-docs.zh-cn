---
title: "使用 SQL Server MicrosoftML 包 |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d6b3c17d4fadf639102c4090fceaabee37276bc2
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>使用 SQL Server MicrosoftML 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction)附带了 Microsoft R Server 和 SQL Server 自 2017 年的程序包中包括多个机器学习算法。 这些 Api 为内部的机器学习应用程序，由 Microsoft 已开发且已完善多年来支持高性能大数据，使用多核处理和快速数据流式处理。 MicrosoftML 还包括对文本和图像处理的大量转换。

在 SQL Server 自 2017 年 1 CTP 2.0 中，Python 语言添加了支持。 **Microsoftml**打包 Python 函数等效于 MicrosoftML 包中包含的。 

+ **MicrosoftML for R**

    简介和包的引用： [MicrosoftML： 机器学习 R 算法](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    由于 R 是区分大小写，因此请确保加载包时正确引用的名称。

+ **microsoftml for Python**

    简介和包的引用： [microsoftml （Python 函数库）](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。 

## <a name="whats-in-microsoftml"></a>中的 MicrosoftML

MicrosoftML 包含各种机器学习算法和经过优化的性能的转换。

### <a name="machine-learning-algorithms"></a>机器学习算法

-  线性模型：`rxFastLinear`线性学习器基于随机可以用于二元分类或回归双重坐标上升。 此模型支持 L1 和 L2 正则化。

- 决策树和决策林模型：`rxFastTree`是最初称为 FastRank，开发的目标是在 Bing 中使用提升的决策树算法。 它是最快速和最流行的学习器之一。 支持二元分类和回归。

  `rxFastForest`逻辑回归模型取决于随机林方法。 它相当于 RevoScaleR 中的 `rxLogit` 函数，但支持 L1 和 L2 正则化。 支持二元分类和回归。

- 逻辑回归：`rxLogisticRegression`是一个逻辑回归模型类似于`rxLogit`RevoScaleR 中的额外支持 L1 和 L2 正则化的函数。 支持二进制或多类分类。

- 神经网络：`rxNeuralNet`函数支持二进制分类、 多类分类和使用神经网络回归。 使用 GPU 加速，使用单个 GPU 的可自定义和支持复杂的网络。

- 异常检测。  `rxOneClassSvm`函数基于 SVM 方法，但已针对不平衡数据集中的二元分类进行优化。

### <a name="transformation-functions"></a>转换函数

MicrosoftML 包括大量的专用的功能，可用于将数据转换以及提取功能。

- 文本处理功能包括`featurizeText`和`getSentiment`函数。 你可以计数 n 元语法、 检测，所用的语言或执行文本规范化。 你可以执行清除非索引字删除等操作的常见文本，或从文本生成哈希或基于计数的功能。

- 功能选择并在功能转换函数，如`selectFeatures`或`getSentiment`、 分析数据和创建最适用于建模的功能。

- 使用类似于使用分类变量`categorical`或`categoricalHash`，这将分类值转换为索引的阵列，以便更好的性能进行。

- 函数特定于图像处理和分析，如`extractPixels`或`featurizeImage`，让你获取有关映像的最多信息并更快地处理图像。

有关详细信息，请参阅 [MicrosoftML 函数](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。

## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

本部分介绍如何查找和加载 R 和 Python 代码中的包。

+ 默认情况下，与 Microsoft R Server 9.1.0 和 SQL Server 自 2017 年中安装 R 的 MicrosoftML 包。

    如果你通过使用 Microsoft R Server 安装此处所述升级的实例的 R 组件，它是还可与 SQL Server 2016 一起使用：[使用绑定的 SQL Server 实例升级](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ **Microsoftml**包安装适用于 Python 的默认情况下，与 SQL Server 自 2017 年 

   若要使用此包，我们建议你升级到候选发布版 2 或更高版本。 早期版本已发布 RC1 但库经历了相当多的修订版本，包括对函数名称的更改。 

但是，对于 R 和 Python 下，不加载包默认设置。因此，你必须显式加载此包，作为你的代码以使用它的功能的一部分。

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>从 SQL Server 中的 R 调用 MicrosoftML 函数

在 R 代码中，加载 MicrosoftML 包并调用其函数，如任何其他包。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**说明**

+ 与通过 RevoScaleR 包提供的数据处理管道完全集成 MicrosoftML 包。 因此，你可以在任何基于 Windows 的计算上下文，包括已启用的机器学习扩展的 SQL Server 的实例中使用 MicrosoftML 包。

    但是，MicrosoftML 需要对 RevoScaleR 和为了使用远程其函数的引用计算上下文。

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>从 SQL Server 中的 Python 调用 microsoftml 函数

若要从包，在 Python 代码中，调用的函数导入**microsoftml**包，并导入**revoscalepy**如果你需要使用远程计算上下文或相关的连接或数据源对象。 然后，引用所需的各个功能。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**说明**

+ 在 SQL Server 2017 **microsoftml**是 Python35 兼容模块。 

+ 中的函数**microsoftml**与所支持的计算上下文和数据源集成**revoscalepy**。 因此，你可以使用**microsoftml** Python 包来创建和评分从模型中任何基于 Windows 的计算上下文，包括了机器学习扩展插件的 SQL Server 的实例。 启用。

    但是， **microsoftml** for Python 要求对引用**revoscalepy**和其函数，才能使用远程计算上下文。

有关 revoscalepy 的详细信息，请参阅：

+ [什么是 revoscalepy](python/what-is-revoscalepy.md)

+ [revoscalepy 函数库](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
