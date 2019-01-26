---
title: RevoScaleR R 函数库的 SQL Server 机器学习服务
description: 在 SQL Server 2016 R Services 和的 SQL Server 2017 机器学习服务中的 RevoScaleR 函数库介绍
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c67fd63af6ed3492b8064be037ed4f8f5dff338f
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044404"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR （SQL Server 中的 R 库）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR**是来自 Microsoft 的高性能数据科学函数库。 函数支持数据导入、 数据转换、 汇总、 可视化和分析。

与基础 R 函数，可以对大型数据集，以并行和分布式的文件系统上执行 RevoScaleR 操作。 函数可对无法容纳在内存中通过使用块区并通过组装结果时操作完成的数据集运行。

RevoScaleR 函数均用标示出来**rx**或**Rx**前缀以使其容易识别。

RevoScaleR 充当用于分布式的数据科学平台。 例如，您可以使用 RevoScaleR 计算上下文和转换与最先进的算法[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)。 此外可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)来并行运行基础 R 函数。

## <a name="full-reference-documentation"></a>完整的参考文档

**RevoScaleR**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[各个 RevoScaleR 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)发布到下一个位置[R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="versions-and-platforms"></a>版本和平台

**RevoScaleR**库是根据 R 3.4.3 和可用，仅在安装以下 Microsoft 产品或下载之一：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 完整的产品发布版本是 Windows 限、 从 SQL Server 2017 开始。 针对 Linux 支持**RevoScaleR**中的新[SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="functions-by-category"></a>按类别列出的函数

本节按类别，以便您了解如何使用每个列出的函数。 此外可以使用[目录](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)来按字母顺序查找函数。

## <a name="1-data-source-and-compute"></a>1-数据源和计算

**RevoScaleR**包括用于创建数据源并将位置设置的函数或*计算上下文*，在其中执行计算。 数据源对象是一个容器，它指定了连接字符串以及你需要的以表、视图或查询格式定义的数据集。 不支持存储过程调用。 下表列出了与 SQL Server 方案相关的函数。

SQL Server 和 R 在某些情况下使用不同的数据类型。 有关 SQL 和 R 数据类型之间的映射的列表，请参阅[R 到 SQL 数据类型](r-libraries-and-data-types.md)。

| 函数| Description|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  创建将计算推送到远程实例的 SQL Server 计算上下文对象。 多个**RevoScaleR**函数采用作为自变量的计算上下文。 |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 获取或设置活动计算上下文。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 创建基于 SQL Server 查询或表的数据对象。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 创建基于 ODBC 连接的数据源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 创建基于本地 XDF 文件的数据源。 XDF 文件通常用于内存中将数据卸载到磁盘。 在使用更多的数据不是可以从一个批处理中的数据库传输或更多的数据多于可以容纳在内存中时，XDF 文件很有用。 例如，如果您定期大量数据从数据库移动到本地工作站，而不是查询重复的每个 R 操作，数据库可 XDF 文件作为缓存的一种保存数据保存在本地，然后使用它在 R 工作区中。|

> [!TIP]
> 如果不熟悉的数据源的想法或计算上下文，我们建议您开始[分布式计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)Microsoft Machine Learning Server 文档中。

### <a name="perform-ddl-statements"></a>执行 DDL 语句

如果必须在实例和数据库的必要权限的情况下，可以从 R 执行 DDL 语句。 以下函数使用 ODBC 调用执行 DDL 语句或检索数据库架构。

| 函数| Description|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | 删除[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]表，或检查是否存在的数据库表或对象。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 执行数据定义语言 (DDL) 命令，它定义或处理数据库对象。 此函数不能返回的数据，并仅用于检索或修改的对象架构或元数据。|

## <a name="2-data-manipulation-etl"></a>2 数据操作 (ETL)

创建数据源对象后，可以使用对象来将数据加载到其中，转换数据，或将新数据写入到指定的目标。 你还可以根据源中的数据大小将批大小定义为数据源的一部分，并成块移动数据。

| 函数 | Description |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 检查数据源是否可用，请打开或关闭数据源、 从源读取数据、 将数据写入到目标，并关闭数据源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 将数据数据从源分片移动到文件存储或数据帧。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 数据源之间移动时转换数据。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3 绘图函数

| 函数名称 | Description |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |从数据创建直方图。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |从数据创建线图。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |计算可绘制的 Lorenz 曲线。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |计算并绘制 ROC 曲线实际和预测数据。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 描述性统计信息

| 函数名称 | Description |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |计算近似分位数的.xdf 文件和数据帧而不进行排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |数据，包括按组进行计算的基本摘要统计信息。 写入到不受支持的.xdf 文件组计算的。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |基于公式的交叉表的数据。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |替代基于公式的交叉表用于返回多维数据集结果的有效表示形式。 输出写入到.xdf 文件不受支持。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |跨 tabulations 边际摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |将交叉表结果到 xtabs 对象。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 对象上执行卡方检验。 适用于小型数据集，不分块数据。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |对 xtabs 对象执行四格表精确检验。 适用于小型数据集，不分块数据。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |计算肯德尔等级相关系数使用 xtabs 对象。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |将函数应用到成对组合的行和列 xtabs 对象。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算两个由两个 xtabs 对象的相对风险。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算两个由两个 xtabs 对象的比值比。 | 

<sup>*</sup> 表示此类别中最常用的函数。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5 预测函数

| 函数名称 | Description |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |适合于数据的线性模型。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |适合于数据的逻辑回归模型。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |适合于数据的通用线性模型。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |计算的协方差、 相关的更多信息或总和的平方 / 叉积矩阵的一组变量。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |适用于数据的分类或回归树。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |适用于使用随机渐进提升算法对数据的决策林分类或回归。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |适用于数据的分类或回归决策林。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |计算拟合模型的预测。 输出必须 XDF 数据源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |执行 k 平均值聚类分析。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |执行 Naive Bayes 分类。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |计算一组变量的协方差矩阵。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算一组变量的相关矩阵。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算总和的平方 / 叉积矩阵的一组变量。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |接收者操作特性 (ROC) 计算使用从二元分类器系统的实际和预测值。 | 

<sup>*</sup> 表示此类别中最常用的函数。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

中的函数**RevoScaleR**是可封装在存储过程的 R 代码中调用。 大多数开发人员构建**RevoScaleR**解决方案本地，然后将完成的 R 代码迁移到存储过程作为部署练习。

本地运行时，通常要运行 R 脚本，从命令行中，或从 R 开发环境，并指定使用一个 SQL Server 计算上下文**RevoScaleR**函数。 您可以使用远程计算上下文，对于整个代码中，或有关各个函数。 例如，你可能想要卸载到服务器以使用最新数据并避免数据移动的模型定型。

当你准备好将封装在存储过程中，R 脚本[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我们建议为清晰地定义了输入和输出的单个函数重写代码。 

## <a name="see-also"></a>另请参阅

+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [面向 SQL 开发人员的 R:训练和操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 引用 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
