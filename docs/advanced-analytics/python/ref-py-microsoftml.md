---
title: microsoftml Python 包的 SQL Server 机器学习服务
description: 引入了 Microsoft 机器学习算法和 python，模型与 SQL Server 机器学习工作负荷相关。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b892af192be2cea441004adca8e9297f1947b313
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645087"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml （SQL Server 中的 Python 模块）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml**是 Microsoft 提供高性能的计算机学习算法提供 Python35 兼容的模块。 它包括用于培训和转换、 评分、 文本和图像分析和特征提取用于从现有数据派生值的函数。

机器学习 Api 由 Microsoft 内部的机器学习应用程序的开发和了而优化多年来支持高性能大数据，使用多核处理和快速数据流。 此包的 R 版本，一种 Python 等效于源自[MicrosoftML](../r/ref-r-microsoftml.md)，具有相似的功能。 

## <a name="full-reference-documentation"></a>完整的参考文档

**Microsoftml**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[单个 microsoftml 函数的文档](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)发布到下一个位置[Python 参考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="versions-and-platforms"></a>版本和平台

**Microsoftml**模块是基于 Python 3.5 和可用，仅在安装以下 Microsoft 产品或下载之一：

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [数据科学客户端的 Python 客户端库](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整的产品发布版本是 Windows 限、 从 SQL Server 2017 开始。 针对 Linux 支持**microsoftml**中的新[SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="package-dependencies"></a>包的依赖项

中的算法**microsoftml**依赖于[revoscalepy](ref-py-revoscalepy.md)为：

+ 数据源对象。 通过使用数据**microsoftml**函数使用创建**revoscalepy**函数。
+ 远程计算 （不断变化函数执行到远程 SQL Server 实例）。 **Revoscalepy**库提供了函数，创建并激活远程计算上下文的 SQL server。

在大多数情况下，您将加载的包一起每当你使用**microsoftml**。

## <a name="functions-by-category"></a>按类别列出的函数

本节按类别，以便您了解如何使用每个列出的函数。 此外可以使用[目录](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)来按字母顺序查找函数。

## <a name="1-training-functions"></a>1-训练函数

| 函数 | Description |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 训练模型的系综。 |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 随机林。 |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 线性模型。 与随机双坐标上升。 |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 提升的树。 |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 逻辑回归。 |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 神经网络。 |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 异常情况检测。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-转换函数

### <a name="categorical-variable-handling"></a>分类变量的处理

| 函数 | Description |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 将文本列转换为类别。 |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 哈希处理并将文本列转换为类别。 |

### <a name="schema-manipulation"></a>架构操作

| 函数 | Description |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 将多个列连接成单个向量。 |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 从数据集中删除列。 |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 将保留数据集的列。 |


### <a name="variable-selection"></a>变量选择

| 函数 | Description |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |基于计数的特征选择。 |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 功能选择基于互信息。 |


### <a name="text-analytics"></a>文本分析

| 函数 | Description |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 将文本列转换成数字特征。 |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 情绪分析。 |


### <a name="image-analytics"></a>图像分析 

| 函数 | Description |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 加载图像。 |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 调整图像大小。 |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 从图像中提取像素为单位。 |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 将图像转换为功能。 |

### <a name="featurization-functions"></a>特征化函数

| 函数 | Description |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 数据源的数据转换 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3 评分函数

| 函数 | Description |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | 使用 Microsoft 机器学习模型评分 |

## <a name="how-to-call-microsoftml"></a>如何调用 microsoftml

中的函数**microsoftml**是可封装在存储过程的 Python 代码中调用。 大多数开发人员构建**microsoftml**解决方案本地，然后将完成的 Python 代码作为部署练习迁移到存储过程。

**Microsoftml**默认情况下，但不同于安装 Python 包**revoscalepy**，它时不会加载默认情况下启动 Python 会话使用随 SQL Server 安装的 Python 可执行文件。

第一步中，导入**microsoftml**包，并导入**revoscalepy**您是否需要使用远程计算上下文或相关的连接或数据源对象。 然后，引用所需的各个函数。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另请参阅

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)
+ [教程：在 T-SQL 中嵌入 Python 代码](../tutorials/run-python-using-t-sql.md)
+ [Python 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

