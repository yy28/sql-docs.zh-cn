---
title: microsoftml Python 包
description: 介绍了适用于 Python 的 Microsoft 机器学习算法和模型, 与 SQL Server 机器学习工作负载相关。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 298328db563cac8183b14b47e5c75c850c782d58
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345460"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (SQL Server 中的 Python 模块)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml**是 Microsoft 提供的 Python35 兼容模块, 提供高性能机器学习算法。 它包括用于定型和转换、计分、文本和图像分析的函数以及用于从现有数据派生值的功能提取。

机器学习 Api 是由 Microsoft 为内部机器学习应用程序开发的, 多年来, 使用多核处理和快速数据流来支持大数据的高性能。 此包是作为具有类似功能的 R 版本[MicrosoftML](../r/ref-r-microsoftml.md)的 Python 等效的。 

## <a name="full-reference-documentation"></a>完整参考文档

**Microsoftml**库分布在多个 Microsoft 产品中, 但不管你是在 SQL Server 还是在其他产品中获取库, 使用情况都是相同的。 由于函数是相同的, 因此[每个 microsoftml 函数的文档](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)仅发布到 Microsoft Machine Learning Server 的[Python 参考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)中的一个位置。 如果存在任何特定于产品的行为, 则函数帮助页中将注明差异。

## <a name="versions-and-platforms"></a>版本和平台

**Microsoftml**模块基于 Python 3.5, 仅在安装以下 Microsoft 产品或下载之一时可用:

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [用于数据科学客户端的 Python 客户端库](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整产品发布版本仅限 Windows, 从 SQL Server 2017 开始。 [SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)中新增了对**microsoftml**的 Linux 支持。

## <a name="package-dependencies"></a>包依赖关系

**Microsoftml**中的算法依赖于[revoscalepy](ref-py-revoscalepy.md) :

+ 数据源对象。 **Microsoftml**函数使用的数据是使用**revoscalepy**函数创建的。
+ 远程计算 (将函数执行转移到远程 SQL Server 实例)。 **Revoscalepy**库提供了用于为 SQL server 创建和激活远程计算上下文的函数。

在大多数情况下, 只要使用**microsoftml**, 就会将包加载到一起。

## <a name="functions-by-category"></a>按类别列出的函数

本部分列出了按类别列出的功能, 以帮助您了解每个函数的使用方式。 你还可以使用[目录](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)按字母顺序查找函数。

## <a name="1-training-functions"></a>1-定型函数

| Functions | 描述 |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 训练模型的系综。 |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 随机林。 |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 线性模型。 with 随机双坐标升高。 |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 提升树。 |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 逻辑回归。 |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 神经网络。 |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 异常检测。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2转换函数

### <a name="categorical-variable-handling"></a>分类变量处理

| Functions | 描述 |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 将文本列转换为类别。 |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 将文本列哈希和转换为类别。 |

### <a name="schema-manipulation"></a>架构操作

| Functions | 描述 |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 将多个列串联为一个向量。 |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 从数据集中删除列。 |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 保留数据集的列。 |


### <a name="variable-selection"></a>变量选择

| Functions | 描述 |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |基于计数的功能选择。 |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 基于相互信息的功能选择。 |


### <a name="text-analytics"></a>文本分析

| Functions | 描述 |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 将文本列转换为数字特征。 |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 情绪分析。 |


### <a name="image-analytics"></a>映像分析 

| Functions | 描述 |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 加载图像。 |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 调整图像大小。 |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 从图像中提取像素。 |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 将图像转换为特征。 |

### <a name="featurization-functions"></a>特征化函数

| Functions | 描述 |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 数据源的数据转换 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-计分函数

| Functions | 描述 |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | 使用 Microsoft 机器学习模型评分 |

## <a name="how-to-call-microsoftml"></a>如何调用 microsoftml

**Microsoftml**中的函数可在存储过程中封装的 Python 代码中调用。 大多数开发人员在本地生成**microsoftml**解决方案, 然后将完成的 Python 代码迁移到存储过程以进行部署。

默认情况下, 将安装 Python 的**microsoftml**包, 但与**revoscalepy**不同的是, 当你使用随 SQL Server 安装的 python 可执行文件启动 python 会话时, 默认情况下不会加载它。

第一步是导入**microsoftml**包, 并导入**revoscalepy** (如果需要使用远程计算上下文或相关连接或数据源对象)。 然后, 引用所需的各个函数。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>请参阅

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)
+ [教程：在 T-sql 中嵌入 Python 代码](../tutorials/run-python-using-t-sql.md)
+ [Python 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

