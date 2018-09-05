---
title: 将 MicrosoftML 包与 SQL Server 使用 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a75ed22e46576c701e281f495d5bc123ca489526
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348458"
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>将 MicrosoftML 包与 SQL Server 使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction)随附 Microsoft R Server 和 SQL Server 2017 的程序包中包括多个机器学习算法。 这些 Api 对内部机器学习应用程序，由 Microsoft 开发，已优化多年来支持高性能大数据，使用多核处理和快速数据流。 MicrosoftML 还包括文本和图像处理的大量转换。

在 SQL Server 2017 中，已添加对 Python 语言支持。 **Microsoftml**打包 Python 函数等效于 MicrosoftML 包中包含的。 

+ **MicrosoftML for R**

    简介和包的引用： [MicrosoftML： 机器学习 R 算法](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    由于 R 是区分大小写，因此请确保加载包时正确引用名称。

+ **用于 Python 的 microsoftml**

    简介和包的引用： [microsoftml （适用于 Python 的函数库）](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。 

## <a name="whats-in-microsoftml"></a>中的 MicrosoftML

MicrosoftML 包含各种机器学习算法和已针对性能进行优化的转换。

### <a name="machine-learning-algorithms"></a>机器学习算法

-  线性模型：`rxFastLinear`线性学习器基于可用于二元分类或回归的随机双坐标上升。 此模型支持 L1 和 L2 正则化。

- 决策树和决策林模型：`rxFastTree`是最初称为 FastRank，为必应开发一种提升的决策树算法。 它是最快速和最流行的学习器之一。 支持二元分类和回归。

  `rxFastForest` 逻辑回归模型为基础的随机林方法。 它相当于 RevoScaleR 中的 `rxLogit` 函数，但支持 L1 和 L2 正则化。 支持二元分类和回归。

- 逻辑回归：`rxLogisticRegression`是一个逻辑回归模型类似于`rxLogit`中 RevoScaleR，提供其他支持 L1 和 L2 正则化的函数。 支持二元或多类分类。

- 神经网络：`rxNeuralNet`函数支持二元分类、 多类分类和回归使用神经网络。 使用 GPU 加速，使用单个 GPU 的可自定义和支持复杂的网络。

- 异常情况检测。  `rxOneClassSvm`函数基于 SVM 方法，但已针对不均衡数据集中二元分类进行优化。

### <a name="transformation-functions"></a>转换函数

MicrosoftML 包括可用于对数据进行转换和提取功能的多个专用的函数。

- 文本处理功能包括`featurizeText`和`getSentiment`函数。 可以计数的 n 元语法、 检测语言使用，还是执行文本规范化。 此外可以执行清理操作，如非索引字删除常用的文本或从文本生成哈希或基于计数的功能。

- 功能选择和功能转换函数，如`selectFeatures`或`getSentiment`、 分析数据并创建最适用于建模的功能。

- 使用类似于使用分类变量`categorical`或`categoricalHash`，这将分类值转换为更好的性能的索引数组。

- 函数特定于图像处理和分析，如`extractPixels`或`featurizeImage`，可让你获取有关映像的大部分信息和更快地处理映像。

有关详细信息，请参阅 [MicrosoftML 函数](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。

## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

本部分介绍如何查找和加载 R 和 Python 代码中的包。

+ 默认情况下，使用 Microsoft R Server 9.1.0 和 SQL Server 2017 中安装了 R 的 MicrosoftML 包。

    它也是可用于 SQL Server 2016 中，如果使用 Microsoft R Server 安装程序此处所述升级 R 组件的实例：[使用绑定的 SQL Server 实例升级](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ **Microsoftml**默认情况下使用 SQL Server 2017 安装 Python 包 

   若要使用此包，我们建议您升级到候选发布 2 或更高版本。 Rc1 已发布的早期版本，但库经历了大量修订版本，包括对函数名称的更改。 

但是，对 R 和 Python，不加载包默认设置。因此，必须显式代码以使用其功能的一部分加载包。

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>从 SQL Server 中的 R 调用 MicrosoftML 函数

在 R 代码中，加载 MicrosoftML 包并调用其功能，像任何其他包一样。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**说明**

+ 与数据处理管道 RevoScaleR 包提供的完全集成的 MicrosoftML 包。 因此，您可以在任何基于 Windows 的计算上下文，包括已启用的机器学习扩展的 SQL Server 的实例中使用 MicrosoftML 包。

    但是，MicrosoftML 需要对 RevoScaleR 和其功能才能使用远程计算上下文。

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>从 SQL Server 中的 Python 调用 microsoftml 函数

若要从包中，在 Python 代码中，调用的函数导入**microsoftml**包，并导入**revoscalepy**如果需要使用远程计算上下文或相关的连接或数据源对象。 然后，引用所需的各个函数。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**说明**

+ 在 SQL Server 2017 **microsoftml**是 Python35 兼容模块。 

+ 中的函数**microsoftml**与支持的计算上下文和数据源集成**revoscalepy**。 因此，您可以使用**microsoftml** Python 包创建，并从任何基于 Windows 的计算上下文，包括具有机器学习扩展的 SQL Server 的实例中的模型评分。 已启用。

    但是， **microsoftml**的 Python 需要引用**revoscalepy**和其功能才能使用远程计算上下文。

Revoscalepy 有关的详细信息，请参阅：

+ [Revoscalepy 是什么](python/what-is-revoscalepy.md)

+ [revoscalepy 函数库](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
