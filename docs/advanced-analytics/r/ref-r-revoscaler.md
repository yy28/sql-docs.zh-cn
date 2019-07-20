---
title: RevoScaleR R 函数库
description: SQL Server 2016 R Services 中的 RevoScaleR 函数库简介和 SQL Server 2017 机器学习服务 with R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 24c751051ff09fa80e738fc4723a00722b6b2e12
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344527"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (SQL Server 中的 R 库)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR**是 Microsoft 的高性能数据科学函数的库。 函数支持数据导入、数据转换、汇总、可视化和分析。

与基本 R 函数相比, 可以对非常大的数据集并行执行 RevoScaleR 操作, 也可以在分布式文件系统上执行。 函数可以在操作完成时, 通过使用分块并通过 reassembling 的结果, 对在内存中无法容纳的数据集进行操作。

使用**rx**或**rx**前缀来表示 RevoScaleR 函数, 使其易于识别。

RevoScaleR 充当分布式数据科学的平台。 例如, 可以在[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)中将 RevoScaleR 计算上下文和转换用于先进的算法。 还可以使用[rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec)并行运行基本 R 函数。

## <a name="full-reference-documentation"></a>完整参考文档

**RevoScaleR**库分布在多个 Microsoft 产品中, 但不管你是在 SQL Server 还是在其他产品中获取库, 使用情况都是相同的。 由于函数相同, 因此,[每个 RevoScaleR 函数的文档](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)仅发布到 Microsoft Machine Learning Server [R 引用](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)下的一个位置。 如果存在任何特定于产品的行为, 则函数帮助页中将注明差异。

## <a name="versions-and-platforms"></a>版本和平台

**RevoScaleR**库基于 R 3.4.3, 且仅在安装以下 Microsoft 产品或下载之一时可用:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 客户端](set-up-a-data-science-client.md)

> [!NOTE]
> 完整产品发布版本仅限 Windows, 从 SQL Server 2017 开始。 [SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)中新增了对**RevoScaleR**的 Linux 支持。

## <a name="functions-by-category"></a>按类别列出的函数

本部分列出了按类别列出的功能, 以帮助您了解每个函数的使用方式。 你还可以使用[目录](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)按字母顺序查找函数。

## <a name="1-data-source-and-compute"></a>1-数据源和计算

**RevoScaleR**包括用于创建数据源以及设置执行计算的位置或*计算上下文*的函数。 数据源对象是一个容器，它指定了连接字符串以及你需要的以表、视图或查询格式定义的数据集。 不支持存储过程调用。 下表列出了与 SQL Server 方案相关的函数。

在某些情况下, SQL Server 和 R 使用不同的数据类型。 有关 SQL 与 R 数据类型之间的映射的列表, 请参阅[R 到 SQL 数据类型](r-libraries-and-data-types.md)。

| Functions| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  创建 SQL Server 计算上下文对象, 以将计算推送到远程实例。 多个**RevoScaleR**函数采用计算上下文作为参数。 |
|[rxGetComputeContext/rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 获取或设置活动计算上下文。 |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | 创建基于 SQL Server 查询或表的数据对象。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | 基于 ODBC 连接创建数据源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 基于本地 XDF 文件创建数据源。 XDF 文件通常用于将内存中的数据卸载到磁盘。 当使用的数据超过一个批处理中可传输的数据时, 或比内存中容纳的数据更多的数据时, XDF 文件会很有用。 例如, 如果您定期将大量数据从数据库移到本地工作站, 而不是针对每个 R 操作重复查询数据库, 则可以使用 XDF 文件作为缓存来保存数据, 并在 R 工作区中使用它。|

> [!TIP]
> 如果你不熟悉数据源或计算上下文, 我们建议你在 Microsoft Machine Learning Server 文档中开始进行[分布式计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。

### <a name="perform-ddl-statements"></a>执行 DDL 语句

如果对实例和数据库具有必要的权限, 则可以从 R 执行 DDL 语句。 以下函数使用 ODBC 调用来执行 DDL 语句或检索数据库架构。

| Functions| 描述|
| ------- | ---------- |
| [rxSqlServerTableExists 和 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]删除表, 或检查是否存在数据库表或对象。 |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 执行定义或操作数据库对象的数据定义语言 (DDL) 命令。 此函数不能返回数据, 仅用于检索或修改对象架构或元数据。|

## <a name="2-data-manipulation-etl"></a>2-数据操作 (ETL)

创建数据源对象后, 可以使用对象将数据加载到其中, 转换数据, 或者将新数据写入指定的目标。 你还可以根据源中的数据大小将批大小定义为数据源的一部分，并成块移动数据。

| Functions | 描述 |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 检查数据源是否可用、打开或关闭数据源、从源读取数据、将数据写入目标和关闭数据源。|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 将数据从数据源移到文件存储或数据帧中。|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 在数据源之间移动数据时转换数据。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-绘图函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |从数据创建直方图。 | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |从数据创建线条图。 | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |计算可绘制的 Lorenz 曲线。 | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |计算并绘制来自实际数据和预测数据的 ROC 曲线。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-描述性统计信息

| 函数名称 | 描述 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |计算 xdf 文件和数据帧的近似分位数而不进行排序。 | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |数据的基本摘要统计信息, 包括按组计算。 不支持按组计算写入 xdf 文件。 | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |基于公式的交叉表数据。 | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |基于公式的替代交叉表, 用于高效表示返回多维数据集结果。 不支持将输出写入 xdf 文件。 | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |跨 tabulations 的边际摘要。 | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |将交叉表格结果转换为 xtabs 对象。 | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |对 xtabs 对象执行γ平方测试。 用于较小的数据集, 并且不会对数据进行分块。 | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |对 xtabs 对象执行费舍尔的精确测试。 用于较小的数据集, 并且不会对数据进行分块。 | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |使用 xtabs 对象计算肯德尔的 Tau 排名关联系数。 | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |将函数应用于 xtabs 对象的行和列的组合。 | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算 xtabs 对象上的相对风险。 | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |计算两个两个 xtabs 对象的有几率比。 | 

<sup>*</sup>表示此类别中最热门的函数。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-预测函数

| 函数名称 | 描述 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |使线性模型适合数据。 | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |适合数据的逻辑回归模型。 | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)<sup>*</sup> |使通用线性模型适合数据。 | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |计算一组变量的协方差、相关性或平方/叉积矩阵之和。 | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |适合数据的分类或回归树。 | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)<sup>*</sup> |使用随机梯度提升算法, 使分类或回归决策林适应数据。 | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |将分类或回归决策林与数据相适应。 | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |计算拟合模型的预测。 输出必须为 XDF 数据源。 | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans)<sup>*</sup> |执行 k 平均值聚类分析。 | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes)<sup>*</sup> |执行 Naive Bayes 分类。 | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |计算一组变量的协方差矩阵。 | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算一组变量的相关矩阵。 | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |计算一组变量的平方/叉积矩阵之和。 | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |接收器操作特征 (ROC) 使用二进制分类器系统中的实际值和预测值进行计算。 | 

<sup>*</sup>表示此类别中最热门的函数。


## <a name="how-to-work-with-revoscaler"></a>如何使用 RevoScaleR

**RevoScaleR**中的函数可在存储过程中封装的 R 代码中调用。 大多数开发人员在本地生成**RevoScaleR**解决方案, 然后将已完成的 R 代码迁移到存储过程以进行部署。

在本地运行时, 通常从命令行或从 R 开发环境运行 R 脚本, 并使用**RevoScaleR**函数之一指定 SQL Server 计算上下文。 您可以为整个代码或单个函数使用远程计算上下文。 例如, 你可能想要将模型定型卸载到服务器, 以使用最新数据并避免数据移动。

准备好在存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)中封装 R 脚本时, 我们建议将代码重写为一个具有明确定义的输入和输出的函数。 

## <a name="see-also"></a>请参阅

+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [了解如何使用计算上下文](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [适用于 SQL 开发人员的 R:训练和操作模型](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub 上的 Microsoft 产品示例](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
