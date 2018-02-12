---
title: "引入 revoscalepy |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: f6ce9219f2b8969f3bfa7bf96c07cedb7d0c6d90
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="introducing-revoscalepy"></a>引入 revoscalepy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy**提供由 Microsoft，以支持分布式计算、 远程计算上下文和高性能算法 for Python 是一个新的库。

它基于**RevoScaleR** ，提供 Microsoft R Server 和 SQL Server R Services 和旨在提供相同的功能中的包：

+ 支持多个计算上下文，远程和本地
+ 提供了用于数据转换和可视化效果等效于 RevoScaleR 函数
+ 为分布式或并行处理提供 RevoScaleR 机器学习算法的 Python 的版本
+ 提高的性能，包括使用 Intel 数学库

此外为 R 和 Python 提供了 MicrosoftML 包。 有关详细信息，请参阅[SQL Server 中使用 MicrosoftML](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>版本和支持的平台

**Revoscalepy**模块是提供仅当你安装的以下 Microsoft 产品之一：

+ 机器学习中 SQL Server 自 2017 年 1 服务
+ Microsoft 机器学习 Server 9.2.0 或更高版本

若要获取 revoscalepy 的最新版本，请为 SQL Server 2017 安装累积更新 1。 它包括许多改进 Python，包括：

+ 一个新的 Python 函数`rx_create_col_info`，，如获取 SQL Server 的数据源的架构信息[rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)为 
+ 增强功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支持使用的并行方案`RxLocalParallel`计算上下文。 

## <a name="supported-functions-and-data-types"></a>支持的函数和数据类型

本部分概述的 Python 数据类型和支持中的新 Python 函数**revoscalepy**模块，SQL Server 自 2017 年 1 CTP 2.0 版开始。 

释放到日期的 Python 库中的函数的最新列表，请参阅以下链接：

+ [revoscalepy for Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [microsoftml for Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>数据类型、 数据源和计算上下文

SQL Server 和 Python 在某些情况下使用不同的数据类型。 SQL 和 Python 数据类型之间的映射列表，请参阅[Python 库和数据类型](python-libraries-and-data-types.md)。

机器学习与 SQL Server 中的 Python 支持的数据源包括 ODBC 数据源、 SQL Server 数据库和本地文件，包括 XDF 文件。

使用下表中列出的函数来创建数据源对象。 定义数据源后, 加载或转换数据，通过使用适当[ETL 函数](#bkmk_etl)。

> [!IMPORTANT]
> 在 CTP 2.0 中的 Python 初始发布后更改许多函数名。

**SQL Server 数据**

+ 使用[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)定义从查询或表的数据源
+ 使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver)创建 SQL Server 计算上下文
+ 使用[RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata)从 ODBC 连接创建数据源

**revoscalepy**还支持[XDF 数据源](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata)，用于内存和其他数据源之间移动数据。

> [!TIP]
> 如果你不熟悉的数据源的想法，或计算上下文，我们建议你先阅读关于分布式计算适用于机器学习中[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction)。


### <a name="bkmk_algorithms"></a>机器学习和摘要函数

SQL Server 2017，开头 CTP 2.0 中包含的以下机器学习算法和摘要函数从 RevoScaleR。

| 函数| Description|说明|
| ------ | ------ |------ |
|`rx_btrees` | 适合的随机渐变提升决策树|`rx_btrees_ex` in CTP 2.0|
|`rx_dforest` | 适合分类和回归的决策林|`rx_dforest_ex` in CTP 2.0|
|`rx_dtree` | 适合的分类和回归树 |`rx_dtree_ex` in CTP 2.0|
|`rx_lin_mod` | 创建线性模型|`rx_lin_mod_ex` in CTP 2.0|
|`rx_logit` | 创建逻辑回归模型|`rx_logit_ex` in CTP 2.0|
|`rx_predict` | 从训练的模型生成预测|`rx_predict_ex` in CTP 2.0|
|`rx_summary` | 生成模型的摘要||

新的机器学习算法还提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| 函数| Description|
| ------ | ------ |
|`rx_fast_forest` |创建决策林模型|
|`rx_fast_linear` | 使用随机双重坐标上升的线性回归|
|`rx_fast_trees` | 创建提升的树模型 |
|`rx_logistic_regression` | 创建逻辑回归模型|
|`rx_neural_network` | 创建一个可自定义神经网络模型 |
|`rx_oneclass_svm` | 在非平衡数据集，用于异常检测创建 SVM 模型|

> [!TIP]
> 许多这些算法已提供作为 Azure 机器学习中的模块。

For Python MicrosoftML 还包括各种转换和帮助器函数，如：

+ `rx_predict`从训练的模型生成预测，并可用于实时评分
+ 图像特征化函数
+ 文本处理和观点提取函数

有关详细信息，请参阅[MicrosoftML 简介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社区使用可能不同于你使用，包括所有小写字母和下划线，而对于参数名 camel 大小写的编码约定。 此外，可能是你已注意到， **revoscalepy**库始终采用小写形式。 没错！ 另一个 Python 约定。
> 
> 请查看 Microsoft: [Python 函数帮助] 的 Python 参考文档上的提示[Python 函数帮助](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>示例

你可以运行代码，其中包括**revoscalepy**函数本地或远程计算上下文中。 此外可以通过将 Python 代码嵌入在存储过程中运行 SQL Server 内的 Python。

本地运行，通常要从命令行中，或 Python 开发环境中，从运行的 Python 脚本并指定 SQL Server 计算上下文使用之一**revoscalepy**函数。 你可以使用远程计算上下文，对于整个代码中，或各个函数。 例如，你可能想要卸载到服务器以用最新数据，以避免数据移动的模型定型。

如果您想要放置在存储过程中，一个完整的 Python 脚本[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我们建议你重新作为单个函数清楚地定义输入和输出中编写代码。 输入和输出必须**pandas**数据帧。 完成此操作后，可以从支持 T-SQL 的任何客户端调用存储的过程、 轻松地将 SQL 查询传递作为输入，并将结果保存到 SQL 表。 有关示例，请参阅[数据库中的 SQL 开发人员的 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-remote-compute-contexts"></a>使用远程计算上下文

+ [使用 revoscalepy 创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)

  此示例演示如何运行 Python 作为计算上下文中使用的 SQL Server 实例。

### <a name="using-a-stored-procedure"></a>使用存储的过程

+ [运行 Python 使用 T-SQL](../tutorials/run-python-using-t-sql.md)

  此示例演示调用存储过程中嵌入的 Python 脚本的基本机制。

### <a name="using-revoscalepy-with-microsoftml"></a>使用 MicrosoftML revoscalepy

MicrosoftML Python 函数与计算上下文和 revoscalepy 中提供的数据源集成。 因此，您无法使用 MicrosoftML 算法来定义并定型模型以 Python，并使用 revoscalepy 函数来执行 Python 代码，本地或在 SQl Server 计算上下文中。

仅导入你的 Python 代码中的模块，然后引用所需的各个功能。

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>需求

若要在 SQL Server 中运行 Python 代码，你必须已安装 SQL Server 2017 与功能结合**机器学习服务**，并启用 Python 的语言。 早期版本的 SQL Server 不支持 Python 集成。

> [!NOTE]
> Python 的开源分发不支持 SQL Server 计算上下文。 但是，如果你需要发布和使用在 Windows 中的 Python 应用程序，你可以安装 Microsoft 机器学习服务器而无需安装 SQL Server。 有关详细信息，请参阅[创建 a Standalone R Server](../r/create-a-standalone-r-server.md)

## <a name="get-more-help"></a>获取更多帮助

发布产品时，将提供有关这些 Api 的完整文档。 在此期间，我们建议你引用了 RevoScaleR 或 MicrosoftML 的库中的相应函数。

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)。
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

你可以在任何 Python 函数上获取帮助，通过导入模块，然后调用`help()`。 例如，运行`help(revoscalepy)`从你的 Python IDE revoscalepy 模块，使用其签名中返回所有函数的列表。

如果你使用 Python Tools for Visual Studio 时，你可以使用 IntelliSense 获取语法和参数的帮助。 有关详细信息，请参阅[Visual Studio 中的 Python 支持](http://docs.microsoft.com/visualstudio/python/installation)，并下载 Visual Studio 的版本匹配的扩展。 你可以使用 Python 与 Visual Studio 2015 和自 2017 年 1 或更早版本。

## <a name="see-also"></a>另请参阅

[Python 教程](../tutorials/sql-server-python-tutorials.md)
