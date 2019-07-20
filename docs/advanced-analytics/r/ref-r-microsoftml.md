---
title: MicrosoftML R 函数库
description: SQL Server 2016 R Services 中的 MicrosoftML 函数库简介和 SQL Server 2017 机器学习服务 with R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cf89b26ffad2902223a84e19ccaf425aa6f8b2d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344897"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server 中的 R 库)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML**是 Microsoft 提供高性能机器学习算法的 R 函数库。 它包括用于定型和转换、计分、文本和图像分析的函数以及用于从现有数据派生值的功能提取。

机器学习 Api 是由 Microsoft 为内部机器学习应用程序开发的, 多年来, 使用多核处理和快速数据流式处理来支持大数据的高性能。 MicrosoftML 还包括大量文本和图像处理转换。

## <a name="full-reference-documentation"></a>完整参考文档

**MicrosoftML**库分布在多个 Microsoft 产品中, 但不管你是在 SQL Server 还是在其他产品中获取库, 使用情况都是相同的。 由于函数相同, 因此,[每个 RevoScaleR 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)仅发布到 Microsoft Machine Learning Server [R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)下的一个位置。 如果存在任何特定于产品的行为, 则函数帮助页中将注明差异。

## <a name="versions-and-platforms"></a>版本和平台

**MicrosoftML**库基于 R 3.4.3, 且仅在安装以下 Microsoft 产品或下载之一时可用:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 客户端](set-up-a-data-science-client.md)

> [!NOTE]
> 完整产品发布版本仅限 Windows, 从 SQL Server 2017 开始。 [SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)中新增了对**MicrosoftML**的 Linux 支持。

## <a name="package-dependencies"></a>包依赖关系

**MicrosoftML**中的算法依赖于[RevoScaleR](ref-r-revoscaler.md) :

+ 数据源对象。 **MicrosoftML**函数使用的数据是使用**RevoScaleR**函数创建的。
+ 远程计算 (将函数执行转移到远程 SQL Server 实例)。 **RevoScaleR**库提供了用于为 SQL server 创建和激活远程计算上下文的函数。

在大多数情况下, 只要使用**MicrosoftML**, 就会将包加载到一起。

## <a name="functions-by-category"></a>按类别列出的函数

本部分列出了按类别列出的功能, 以帮助您了解每个函数的使用方式。 你还可以使用[目录](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)按字母顺序查找函数。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-机器学习算法

| 函数名称 | 描述 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank 的一个实现, 它是市场渐变提升算法的有效实现。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 使用[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)的随机林和分位回归林实现。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 使用 L-L-BFGS 进行逻辑回归。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 一个类支持向量机。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 二进制、多类和回归神经网络。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 线性二元分类和回归的随机双坐标升高优化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 训练多种不同类型的模型, 以获得比从单个模型获得更好的预测性能。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2转换函数

| 函数名称 | 描述 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 用于从多个列创建单个向量值列的转换。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 通过字典使用分类转换创建指示器向量。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 通过哈希将分类值转换为指示器数组。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 从给定的语料库文本生成连续单词序列的包 (称为 n 语法)。 它提供语言检测、词汇切分、非索引字删除、文本规范化和功能生成。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 为自然语言文本评分并创建一列, 该列包含文本中的情绪为正值的概率。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 允许为基于计数和基于哈希的功能提取定义参数。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 选择一组要重新训练的列, 删除所有其他列。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 使用指定模式从指定的变量中选择功能。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 加载图像数据。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 使用指定的大小调整方法, 将图像大小调整为指定的维度。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 从图像中提取像素值。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 使用预先训练的深神经网络模型 Featurizes 图像。|


## <a name="3-scoring-and-training-functions"></a>3-计分和定型函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 使用存储过程从 SQL Server 运行计分库, 或通过 R 代码运行计分库, 以便提供更快的预测性能。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 将数据从输入数据集转换为输出数据集。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | 提供 Microsoft R 机器学习模型的摘要。|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-分类和回归损失函数

| 函数名称 | 描述 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指数分类损失功能的规范。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 日志分类损失功能的规范。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 枢轴分类损失功能的规范。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平滑转轴分类损失功能的规范。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 泊松回归损失函数的规范。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 方形回归损失函数的规格。   |   

## <a name="5-feature-selection-functions"></a>5-功能选择函数

| 函数名称 | 描述 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 用于在计数模式下选择功能的规范。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 在互信息模式下选择功能的规范。 |

## <a name="6-ensemble-modeling-functions"></a>6-系综建模函数

| 函数名称 | 描述 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 创建一个列表, 其中包含用于使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)训练快速树模型的函数名称和参数。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 创建一个列表, 其中包含用于使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)训练快速林模型的函数名称和参数。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 创建一个列表, 其中包含函数名称和参数, 以使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)为快速线性模型定型。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 创建一个列表, 其中包含用于使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)训练逻辑回归模型的函数名称和参数。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 创建一个列表, 其中包含用于使用[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)训练 OneClassSvm 模型的函数名称和参数。|

## <a name="7-neural-networking-functions"></a>7-神经网络函数

| 函数名称 | 描述 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 指定[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)机器学习算法的优化算法。|


## <a name="8-package-state-functions"></a>8-包状态函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 用于存储包范围状态的环境对象。 |


## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

**MicrosoftML**中的函数可在存储过程中封装的 R 代码中调用。 大多数开发人员在本地生成**MicrosoftML**解决方案, 然后将已完成的 R 代码迁移到存储过程以进行部署。

适用于 R 的**MicrosoftML**包在 SQL Server 2017 中安装 "现成"。 如果升级实例的 R 组件, 还可与 SQL Server 2016 一起使用:[使用绑定升级 SQL Server 的实例](../install/upgrade-r-and-python.md)

默认情况下不加载包。 第一步, 加载**MicrosoftML**包, 然后加载**RevoScaleR** (如果需要使用远程计算上下文或相关连接或数据源对象)。 然后, 引用所需的各个函数。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>请参阅

+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [适用于 SQL 开发人员的 R:训练和操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 