---
title: 引入了 revoscalepy 在 SQL Server 机器学习中的 Python 包 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f1d4d8bbb47c34fce61bdb95a3184a1d2b10f4d1
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889473"
---
# <a name="introducing-revoscalepy-in-sql-server-machine-learning"></a>在 SQL Server 机器学习简介 revoscalepy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy**提供由 Microsoft 以支持分布式计算、 远程计算上下文和高性能算法面向 Python 开发人员是一个新的 Python 库。

它基于**RevoScaleR**对于 R，Microsoft R Server 和 SQL Server R Services，并旨在提供相同的功能中未提供的包：

+ 支持多个计算上下文，远程和本地
+ 提供用于数据转换和可视化效果等效于 RevoScaleR 中的函数
+ 为分布式或并行处理提供 RevoScaleR 机器学习算法的 Python 的版本
+ 改进的性能，其中包括 Intel 数学库的使用

MicrosoftML 包还提供对 R 和 Python。 有关详细信息，请参阅[SQL Server 中使用 MicrosoftML](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>版本和支持的平台

**Revoscalepy**模块是提供仅当您安装以下 Microsoft 产品之一：

+ 机器学习服务，SQL Server 2017 中
+ Microsoft Machine Learning Server 9.2.0 或更高版本

若要获取 revoscalepy 的最新版本，安装 SQL Server 2017 累积更新 1。 它包括了许多改进在 Python 中，包括：

+ 一个新的 Python 函数`rx_create_col_info`，获取架构信息从 SQL Server 数据源，如[rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)为 
+ 增强功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支持使用的并行方案`RxLocalParallel`计算上下文。 

## <a name="supported-functions-and-data-types"></a>支持的函数和数据类型

本部分提供了 Python 数据类型和新的 Python 函数中支持的概述**revoscalepy**模块，SQL Server 2017 CTP 2.0 版本开始。 

截至目前发布的 Python 库中的函数的最新列表，请参阅以下链接：

+ [用于 Python 的 revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [用于 Python 的 microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>数据类型、 数据源和计算上下文

SQL Server 和 Python 在某些情况下使用不同的数据类型。 有关 SQL 和 Python 的数据类型之间的映射的列表，请参阅[Python 扩展](../concepts/extension-python.md)。

使用 Python 在 SQL Server 中机器学习支持的数据源包含 ODBC 数据源、 SQL Server 数据库和本地文件，包括 XDF 文件。

使用下表中列出的函数创建的数据源对象。 定义数据源之后, 加载或转换数据，通过使用合适[ETL 函数](#bkmk_etl)。

> [!IMPORTANT]
> 自 CTP 2.0 中的 Python 的初始版本以来已更改多个函数名称。

**SQL Server 数据**

+ 使用[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)定义来自查询或表的数据源
+ 使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver)创建 SQL Server 计算上下文
+ 使用[RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata)从 ODBC 连接创建数据源

**revoscalepy**还支持[XDF 数据源](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata)，用于内存和其他数据源之间移动数据。

> [!TIP]
> 如果你不熟悉的数据源的想法或计算上下文，我们建议你先阅读有关机器学习中的分布式计算的工作[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)。


### <a name="bkmk_algorithms"></a>机器学习和汇总函数

以下机器学习算法和摘要函数从 RevoScaleR 包含在 SQL Server 2017 中，自 CTP 2.0 起。

| 函数| Description|说明|
| ------ | ------ |------ |
|`rx_btrees` | 适合随机梯度提升的决策树|`rx_btrees_ex` 在 CTP 2.0 中|
|`rx_dforest` | 适合分类和回归的决策林|`rx_dforest_ex` 在 CTP 2.0 中|
|`rx_dtree` | 适合的分类和回归树 |`rx_dtree_ex` 在 CTP 2.0 中|
|`rx_lin_mod` | 创建一个线性模型|`rx_lin_mod_ex` 在 CTP 2.0 中|
|`rx_logit` | 创建逻辑回归模型|`rx_logit_ex` 在 CTP 2.0 中|
|`rx_predict` | 从训练的模型生成预测|`rx_predict_ex` 在 CTP 2.0 中|
|`rx_summary` | 生成模型的摘要||

新的机器学习算法还提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| 函数| Description|
| ------ | ------ |
|`rx_fast_forest` |创建决策林模型|
|`rx_fast_linear` | 使用随机双坐标上升的线性回归|
|`rx_fast_trees` | 创建提升的树模型 |
|`rx_logistic_regression` | 创建逻辑回归模型|
|`rx_neural_network` | 创建一个可自定义神经网络模型 |
|`rx_oneclass_svm` | 创建的不平衡数据集，以便在异常情况检测中使用 SVM 模型|

> [!TIP]
> 许多这些算法已提供作为 Azure 机器学习中的模块。

用于 Python 的 MicrosoftML 还包括各种转换和帮助器函数，如：

+ `rx_predict` 从训练的模型生成预测，并可用于进行实时评分
+ 图像特征化函数
+ 用于文本处理和情绪提取函数

有关详细信息，请参阅[MicrosoftML 简介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社区使用可能不同于你正在使用，包括所有小写字母和下划线，而 camel 大小写格式的参数名称的编码约定。 此外，也许我们发现**revoscalepy**库始终是小写。 没错！ 另一个 Python 约定。
> 
> 请查看有关 Microsoft: [Python 函数帮助] 的 Python 参考文档的提示[Python 函数帮助](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>示例

可以运行代码，其中包括**revoscalepy**函数在本地或远程计算上下文中。 此外可以通过在存储过程中嵌入 Python 代码运行在 SQL Server 内的 Python。

本地运行时，通常要运行的 Python 脚本从命令行中，或从 Python 开发环境，并指定使用一个 SQL Server 计算上下文**revoscalepy**函数。 您可以使用远程计算上下文，对于整个代码中，或有关各个函数。 例如，你可能想要卸载到服务器以使用最新数据并避免数据移动的模型定型。

如果您想要放置在存储过程，一个完整的 Python 脚本[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我们建议作为单个函数的清晰地定义了输入和输出写代码。 必须是输入和输出**pandas**数据帧。 完成此操作后，可以从支持 T-SQL 的任何客户端调用存储的过程、 轻松地传递 SQL 查询作为输入，并将结果保存到 SQL 表。 有关示例，请参阅[面向 SQL 开发人员的数据库内 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-remote-compute-contexts"></a>使用远程计算上下文

+ [使用 revoscalepy 创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)

  此示例演示如何运行 Python 使用的 SQL Server 实例作为计算上下文。

### <a name="using-a-stored-procedure"></a>使用存储的过程

+ [使用 T-SQL 运行 Python](../tutorials/run-python-using-t-sql.md)

  此示例演示如何调用存储过程中嵌入的 Python 脚本的基本机制。

### <a name="using-revoscalepy-with-microsoftml"></a>MicrosoftML 中使用 revoscalepy

MicrosoftML 的 Python 函数计算上下文并 revoscalepy 中提供的数据源与集成。 因此，无法使用 MicrosoftML 算法来定义和在 Python 中，对模型进行定型并 revoscalepy 函数用于本地或在 SQl Server 计算上下文中执行 Python 代码。

只需在 Python 代码中，将模块导入，然后引用所需的各个函数。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>要求

若要在 SQL Server 中运行 Python 代码，您必须已安装 SQL Server 2017 功能以及**机器学习服务**，并启用 Python 语言。 SQL Server 的早期版本不支持 Python 集成。

> [!NOTE]
> Python 开源分发版不支持 SQL Server 计算上下文。 但是，如果你需要发布和使用 Windows 的 Python 应用程序，你可以安装 Microsoft 机器学习服务器而无需安装 SQL Server。 有关详细信息，请参阅[安装 SQL Server 2017 机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)。

## <a name="get-more-help"></a>获取更多帮助

产品发布时，将提供有关这些 Api 的完整文档。 在此期间，我们建议你引用了 RevoScaleR 或 MicrosoftML 的库中的相应函数。

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

可以通过导入模块，然后调用上的任何 Python 函数中获取帮助`help()`。 例如，运行`help(revoscalepy)`从你的 Python IDE revoscalepy 模块，使用它们的签名中返回所有函数的列表。

如果使用 Python Tools for Visual Studio 上时，可以使用 IntelliSense 来获取语法和参数的帮助。 有关详细信息，请参阅[Visual Studio 中的 Python 支持](http://docs.microsoft.com/visualstudio/python/installation)，并下载与你的 Visual Studio 版本匹配的扩展。 可以使用 Python 与 Visual Studio 2015 和 2017 或更早版本。

## <a name="see-also"></a>请参阅

[Python 教程](../tutorials/sql-server-python-tutorials.md)
