---
title: revoscalepy Python 包
description: 有关 Python SQL Server 机器学习服务中的 revoscalepy 模块简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 76c68d0753c4ba29387b3378c1086ce9bce4f53b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715768"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (SQL Server 中的 Python 模块)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy**是 Microsoft 的 Python35 兼容模块, 支持分布式计算、远程计算上下文和高性能数据科学算法。 它基于 R 的**RevoScaleR**包 (与 Microsoft R Server 和 SQL Server R Services 一起分发), 提供类似的功能:

+ 具有相同版本的**revoscalepy**的系统上的本地和远程计算上下文
+ 数据转换和可视化功能
+ 通过分布式或并行处理可缩放的数据科学函数
+ 提高了性能, 包括使用 Intel 数学库

在**revoscalepy**中创建的数据源和计算上下文也可用于机器学习算法。 有关这些算法的简介, 请参阅[SQL Server 中的 Microsoftml Python 模块](ref-py-microsoftml.md)。

## <a name="full-reference-documentation"></a>完整参考文档

**Revoscalepy**库分布在多个 Microsoft 产品中, 但不管你是在 SQL Server 还是在其他产品中获取库, 使用情况都是相同的。 由于函数是相同的, 因此[每个 revoscalepy 函数的文档](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)仅发布到 Microsoft Machine Learning Server 的[Python 参考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)中的一个位置。 如果存在任何特定于产品的行为, 则函数帮助页中将注明差异。

## <a name="versions-and-platforms"></a>版本和平台

**Revoscalepy**模块基于 Python 3.5, 仅在安装以下 Microsoft 产品或下载之一时可用:

+ [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [用于数据科学客户端的 Python 客户端库](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整产品发布版本仅限 Windows, 从 SQL Server 2017 开始。 [SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)中新增了对**revoscalepy**的 Linux 支持。

## <a name="functions-by-category"></a>按类别列出的函数

本部分列出了按类别列出的功能, 以帮助您了解每个函数的使用方式。 你还可以使用[目录](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)按字母顺序查找函数。

## <a name="1-data-source-and-compute"></a>1-数据源和计算

**revoscalepy**包括用于创建数据源以及设置执行计算的位置或*计算上下文*的函数。 下表列出了与 SQL Server 方案相关的函数。

在某些情况下, SQL Server 和 Python 使用不同的数据类型。 有关 SQL 和 Python 数据类型之间的映射的列表, 请参阅[Python 到 SQL 数据类型](python-libraries-and-data-types.md)。

| Functions| 描述|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  创建 SQL Server 计算上下文对象, 以将计算推送到远程实例。 多个**revoscalepy**函数采用计算上下文作为参数。 有关上下文切换示例, 请参阅[使用 Revoscalepy 创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)。|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | 创建基于 SQL Server 查询或表的数据对象。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| 基于 ODBC 连接创建数据源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 基于本地 XDF 文件创建数据源。 XDF 文件通常用于将内存中的数据卸载到磁盘。 当使用的数据超过一个批处理中可传输的数据时, 或比内存中容纳的数据更多的数据时, XDF 文件会很有用。 例如, 如果您定期将大量数据从数据库移到本地工作站, 而不是针对每个 R 操作重复查询数据库, 则可以使用 XDF 文件作为缓存来保存数据, 并在 R 工作区中使用它。 |

> [!TIP]
> 如果你不熟悉数据源或计算上下文, 我们建议你在 Microsoft Machine Learning Server 文档中开始进行[分布式计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。

## <a name="2-data-manipulation-etl"></a>2-数据操作 (ETL)

| Functions | 描述 |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | 将数据导入到 xdf 文件或数据帧。|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 将数据从输入数据集转换为输出数据集。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-定型和摘要

| Functions| 描述|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 调整随机渐变提升决策树|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 调整分类和回归决策林|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 调整分类和回归树 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 创建线性回归模型|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 创建逻辑回归模型|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | 在 revoscalepy 中生成对象的单变量汇总。|

还应查看[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)中的函数以了解其他方法。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4-计分函数

| Functions| 描述|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 从定型模型生成预测|“应用程序适配器” 区域） | 从定型模型生成预测, 并可用于实时评分。 |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 使用 rx_lin_mod 和 rx_logit 对象计算预测值和残差。 |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | 为 rx_dforest 或 rx_btrees 对象中的数据集计算预测值或拟合值。 |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | 为 rx_dtree 对象中的数据集计算预测值或拟合值。 |

## <a name="how-to-work-with-revoscalepy"></a>如何使用 revoscalepy

**Revoscalepy**中的函数可在存储过程中封装的 Python 代码中调用。 大多数开发人员在本地生成**revoscalepy**解决方案, 然后将完成的 Python 代码迁移到存储过程以进行部署。

在本地运行时, 通常从命令行或 Python 开发环境运行 Python 脚本, 并使用**revoscalepy**函数之一指定 SQL Server 计算上下文。 您可以为整个代码或单个函数使用远程计算上下文。 例如, 你可能想要将模型定型卸载到服务器, 以使用最新数据并避免数据移动。

准备好在存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)中封装 Python 脚本时, 我们建议将代码重写为一个具有明确定义的输入和输出的函数。 

输入和输出必须为**pandas**数据帧。 完成此操作后, 你可以从任何支持 T-sql 的客户端调用存储过程, 轻松地将 SQL 查询作为输入传递, 并将结果保存到 SQL 表。 有关示例, 请参阅[了解适用于 SQL 开发人员的数据库内 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-revoscalepy-with-microsoftml"></a>将 revoscalepy 与 microsoftml 配合使用

用于[microsoftml](ref-py-microsoftml.md)的 Python 函数与 revoscalepy 中提供的计算上下文和数据源集成在一起。 在从 microsoftml 调用函数时 (例如, 在定义和定型模型时), 请使用 revoscalepy 函数在本地或在 SQl Server 远程计算上下文中执行 Python 代码。

下面的示例演示用于在 Python 代码中导入模块的语法。 然后, 可以引用所需的各个函数。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>请参阅

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)
+ [教程：在 T-sql 中嵌入 Python 代码](../tutorials/run-python-using-t-sql.md)
+ [Python 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
