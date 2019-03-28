---
title: MicrosoftML R 函数库的 SQL Server 机器学习服务
description: 在 SQL Server 2016 R Services 和的 SQL Server 2017 机器学习服务中的 MicrosoftML 函数库介绍
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 73d9dcf56c0eb5e69704adf169946f6aa28a432c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512254"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML （SQL Server 中的 R 库）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML**是 microsoft 提供高性能的计算机学习算法的 R 函数库。 它包括用于培训和转换、 评分、 文本和图像分析和特征提取用于从现有数据派生值的函数。

机器学习 Api 对内部机器学习应用程序，由 Microsoft 开发和了而优化多年来支持高性能大数据，使用多核处理和快速数据流。 MicrosoftML 还包括文本和图像处理的大量转换。

## <a name="full-reference-documentation"></a>完整的参考文档

**MicrosoftML**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[各个 RevoScaleR 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)发布到下一个位置[R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="versions-and-platforms"></a>版本和平台

**MicrosoftML**库是根据 R 3.4.3 和可用，仅在安装以下 Microsoft 产品或下载之一：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 完整的产品发布版本是 Windows 限、 从 SQL Server 2017 开始。 针对 Linux 支持**MicrosoftML**中的新[SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="package-dependencies"></a>包的依赖项

中的算法**MicrosoftML**依赖于[RevoScaleR](ref-r-revoscaler.md)为：

+ 数据源对象。 通过使用数据**MicrosoftML**函数使用创建**RevoScaleR**函数。
+ 远程计算 （不断变化函数执行到远程 SQL Server 实例）。 **RevoScaleR**库提供了函数，创建并激活远程计算上下文的 SQL server。

在大多数情况下，您将加载的包一起每当你使用**MicrosoftML**。

## <a name="functions-by-category"></a>按类别列出的函数

本节按类别，以便您了解如何使用每个列出的函数。 此外可以使用[目录](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)来按字母顺序查找函数。

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1 机器学习算法

| 函数名称 | Description |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank，MART 渐进提升算法的有效实现一个实现。  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 随机林和分位回归林实现使用[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)。  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 使用 L-BFGS 逻辑回归。  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 一个类支持向量机。  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 二进制文件、 多类和回归神经网络。  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 用于线性二元分类和回归随机双坐标上升优化。 |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 训练的模型以获取更好地预测的性能不是可以从单个模型中获取的不同类型的数。|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2 转换函数

| 函数名称 | Description |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 若要从多个列创建单列矢量值的转换。  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 创建分类转换使用字典的指示器向量。  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 分类值将转换为指示器数组的哈希。 |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 生成的序列的连续单词，从给定文本集内调用 n 元语法计数的包。 它提供了语言检测、 词汇切分、 删除非索引字、 文本规范化和生成功能。  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 自然语言文本进行评分，并创建一列以包含在文本情绪是积极的概率。|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 允许定义基于计数的和基于哈希的特征提取的参数。|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 选择一组列来重新训练，删除所有其他用户。 |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 使用指定的模式的指定变量从选择的功能。|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 加载图像数据。|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 调整到使用指定的调整大小方法指定维度的图像的大小。|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 从图像中提取的像素值。|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 使用预先训练的深度神经网络模型的图像特征化。|


## <a name="3-scoring-and-training-functions"></a>3 评分和培训函数

| 函数名称 | Description |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 从 SQL Server，使用存储的过程或从 R 代码启用实时评分，以提供要快得多的预测性能，请运行评分的库。|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 将数据从输入的数据集到输出数据集的转换。|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | 提供 Microsoft R 机器学习模型的摘要。|


## <a name="4-loss-functions-for-classification-and-regression"></a>用于分类和回归的 4 丢失函数

| 函数名称 | Description |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 指数分类损失函数的规范。 | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 日志分类损失函数的规范。  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 转轴分类损失函数的规范。 | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平滑转轴分类损失函数的规范。  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 泊松回归损失函数的规范。 | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 平方的回归损失函数的规范。   |   

## <a name="5-feature-selection-functions"></a>5 功能选择函数

| 函数名称 | Description |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 计数模式中的功能选择的规范。 |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 互信息模式中的功能选择的规范。 |

## <a name="6-ensemble-modeling-functions"></a>6 系综建模函数

| 函数名称 | Description |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 创建包含的函数名称和参数来训练具有的快速树模型的列表[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 创建包含的函数名称和参数来训练具有的快速林模型的列表[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 创建包含的函数名称和参数来训练具有快速线性模型的列表[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 创建包含的函数名称和参数来训练逻辑回归模型使用的列表[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 创建包含的函数名称和要训练 OneClassSvm 模型使用参数的列表[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)。|

## <a name="7-neural-networking-functions"></a>7 神经网络函数

| 函数名称 | Description |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 指定用于优化算法[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)机器学习算法。|


## <a name="8-package-state-functions"></a>8-包状态函数

| 函数名称 | Description |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 环境对象用于存储包范围的状态。 |


## <a name="how-to-use-microsoftml"></a>如何使用 MicrosoftML

中的函数**MicrosoftML**是可封装在存储过程的 R 代码中调用。 大多数开发人员构建**MicrosoftML**解决方案本地，然后将完成的 R 代码迁移到存储过程作为部署练习。

**MicrosoftML**包为 R 是已安装"--现成的"SQL Server 2017 中。 如果升级 R 组件的实例，它是还可与 SQL Server 2016 一起使用：[使用绑定的 SQL Server 实例升级](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

默认情况下不加载包。 第一步中，加载**MicrosoftML**包，然后再加载**RevoScaleR**您是否需要使用远程计算上下文或相关的连接或数据源对象。 然后，引用所需的各个函数。

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>另请参阅

+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [面向 SQL 开发人员的 R:训练和操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 引用 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 