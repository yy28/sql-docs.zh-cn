---
title: RevoScaleR R 函数库
description: SQL Server 2016 R Services 中的 RevoScaleR 函数库，以及具有 R 的 SQL Server 机器学习服务简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7b24d5499e618a09c4d80e8614b08219e6c6f788
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706758"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR（SQL Server 中的 R 库）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR 是 Microsoft 提供的高性能数据科学函数库  。 这些函数支持数据导入、数据转换、摘要、可视化和分析。

与基本 R 函数相比，RevoScaleR 操作可针对大型数据集以并行方式在分布式文件系统上执行。 函数可以通过使用分块和在操作完成时重组结果来操作未存入内存的数据集。

RevoScaleR 函数用 rx 或 Rx 前缀表示，以便于识别   。

RevoScaleR 可作为分布式数据科学的平台。 例如，可将 RevoScaleR 计算上下文和转换与 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package) 中的最先进算法一起使用。 也可使用 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 并行运行基本 R 函数。

## <a name="full-reference-documentation"></a>完整参考文档

RevoScaleR 库分布于多种 Microsoft 产品中，但不管你是在 SQL Server 还是在其他产品中获取库，使用情况都是一样的  。 由于函数相同，因此[单个 RevoScaleR 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)仅发布到 Microsoft Machine Learning Server 的 [R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)下的一个位置。 如果存在任何特定于产品的行为，这些差异将在函数帮助页中注明。

## <a name="versions-and-platforms"></a>版本和平台

RevoScaleR 库基于 R 3.4.3，且仅在安装以下 Microsoft 产品或下载之一时才可用  ：

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> 完整产品发布版本为 SQL Server 2017（仅限 Windows）。 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) 中的 RevoScaleR 同时支持 Windows 和 Linux  。

## <a name="functions-by-category"></a>按类别列出函数

本部分按类别列出函数，以帮助了解每个函数的使用方式。 此外，还可以使用[目录](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)按字母顺序查找函数。

## <a name="1-data-source-and-compute"></a>1 数据源和计算

RevoScaleR 包含用于创建数据源和设置执行计算的位置或计算上下文的函数   。 数据源对象是一个容器，它指定了连接字符串以及你需要的以表、视图或查询格式定义的数据集。 不支持存储过程调用。 下表列出了与 SQL Server 方案相关的函数。

在某些情况下，SQL Server 和 R 使用不同的数据类型。 有关 SQL 和 R 数据类型之间的映射的列表，请参阅 [R 到 SQL 数据类型](r-libraries-and-data-types.md)。

| 函数| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  创建 SQL Server 计算上下文对象以将计算推送到远程实例。 好几个 RevoScaleR 函数都将计算上下文作为参数  。 |
|[rxGetComputeContext/rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 获取或设置活动计算上下文。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 基于 SQL Server 查询或表创建数据对象。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 基于 ODBC 连接创建数据源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 基于本地 XDF 文件创建数据源。 XDF 文件通常用于将内存中数据卸载到磁盘。 当处理的数据多于可以在一批中从数据库传输的数据时，或者数据多于内存中可以容纳的数据时，XDF 文件可能比较有用。 例如，如果定期将大量数据从数据库移动到本地工作站，而非针对每个 R 操作重复查询数据库，则可以使用 XDF 文件作为缓存将数据保存在本地，然后在 R 工作区中使用它。|

> [!TIP]
> 如果不熟悉数据源或计算上下文，建议从 Microsoft Machine Learning Server 文档中的[分布式计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)开始。

### <a name="perform-ddl-statements"></a>执行 DDL 语句

如果你在实例和数据库上具有所需的权限，则还可以从 R 执行 DDL 语句。 以下函数使用 ODBC 调用执行 DDL 语句或检索数据库架构。

| 函数| 描述|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | 删除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 表，或检查是否存在某个数据库表或对象。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 执行定义或操作数据库对象的数据定义语言 (DDL) 命令。 此函数无法返回数据，仅用于检索或修改对象架构或元数据。|

## <a name="2-data-manipulation-etl"></a>2 数据操作 (ETL)

创建数据源对象后，可使用该对象将数据加载到其中，转换数据或将新数据写入指定目标。 你还可以根据源中的数据大小将批大小定义为数据源的一部分，并成块移动数据。

| 函数 | 描述 |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 检查数据源是否可用、打开或关闭数据源、从源读取数据、向目标写入数据以及关闭数据源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 将数据从数据源移动到文件存储或数据帧中。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 在数据源之间移动数据时转换数据。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3 绘图函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |使用数据创建直方图。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |使用数据创建线图。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |计算可绘制的 Lorenz 曲线。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |使用实际数据和预测数据计算并绘制 ROC 曲线。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 描述性统计信息

| 函数名称 | 描述 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |计算 .xdf 文件和数据帧的近似分位数，但不排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |数据的基本摘要统计信息，包括按组进行的计算。 不支持将按组进行的计算写入 .xdf 文件。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |基于公式的数据交叉表。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |基于可替代分子式的交叉表，旨在有效地表示返回的多维数据集结果。 不支持将输出写入 .xdf 文件。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |交叉表的边际摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |将交叉表结果转换为 xtab 对象。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |对 xtab 对象进行卡方检验。 用于小型数据集，不对数据进行分块。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |对 xtab 对象进行四格表精确检验。 用于小型数据集，不对数据进行分块。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |使用 xtab 对象计算肯德尔等级相关系数。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |将函数应用到 xtab 对象成对组合的行和列。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算 xtab 对象两两组合的相对风险。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算 xtab 对象两两组合的比值比。 | 

<sup>* </sup> 表示该类别中最受欢迎的函数。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5 预测函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |调整线性模型以适应数据。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |调整逻辑回归模型以适应数据。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |调整通用线性模型以适应数据。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |计算一组变量的协方差、相关性或平方和/叉积矩阵。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |调整分类或回归树以适应数据。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |使用随机梯度提升算法调整分类或回归决策林以适应数据。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |调整分类或回归决策林以适应数据。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |计算拟合模型的预测。 输出必须为 XDF 数据源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |进行 K-Means 聚类分析。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |进行 Naive Bayes 分类。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |计算一组变量的协方差矩阵。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算一组变量的相关矩阵。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算一组变量的平方和/叉积矩阵。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |使用二进制分类器系统中的实际值和预测值计算接收器操作特征 (ROC) | 

<sup>* </sup> 表示该类别中最受欢迎的函数。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

可在存储过程中封装的 R 代码中调用 RevoScaleR 中的函数  。 大多数开发者会在本地构建 RevoScaleR 解决方案，然后将已完成的 R 代码迁移到存储过程作为部署练习  。

在本地运行时，通常可在命令行或 R 开发环境中运行 R 脚本，并使用 RevoScaleR 函数之一指定 SQL Server 计算上下文  。 可将远程计算上下文用于整个代码或单个函数。 例如，你可能希望将模型定型卸载到服务器上以使用最新数据并避免数据移动。

准备好将 R 脚本封装在存储过程 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 中时，建议将代码重写为具有明确定义的输入和输出的单个函数。 

## <a name="see-also"></a>另请参阅

+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [面向 SQL 开发者的 R：定型和操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 引用 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
