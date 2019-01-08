---
title: revoscalepy Python 包的 SQL Server 机器学习服务
description: 与 Python 配合使用的 SQL Server 2017 机器学习服务中的 revoscalepy 模块简介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b204ab644e4b454bc3671801f32b089a8210c521
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645168"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy （SQL Server 中的 Python 模块）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy**是 Microsoft 支持分布式计算的、 远程计算上下文和高性能数据科学算法提供 Python35 兼容的模块。 它基于**RevoScaleR** R （使用 Microsoft R Server 和 SQL Server R Services 分发）、 产品/服务类似的功能的包：

+ 本地和远程计算上下文在具有相同版本的系统上**revoscalepy**
+ 数据转换和可视化函数
+ 数据科学函数，可通过分布式或并行处理缩放
+ 改进的性能，其中包括 Intel 数学库的使用

数据源和您在中创建的计算上下文**revoscalepy**还可以在机器学习算法中使用。 有关这些算法的简介，请参阅[microsoftml SQL Server 中的 Python 模块](ref-py-microsoftml.md)。

## <a name="full-reference-documentation"></a>完整的参考文档

**Revoscalepy**库分布在多个 Microsoft 产品，但使用情况都是相同是否获取 SQL Server 或另一个产品中的库。 函数是相同的因为[单个 revoscalepy 函数的文档](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)发布到下一个位置[Python 参考](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)的 Microsoft Machine Learning Server。 应任何特定于产品的行为存在，请将函数的帮助页中所示的差异。

## <a name="versions-and-platforms"></a>版本和平台

**Revoscalepy**模块是基于 Python 3.5 和可用，仅在安装以下 Microsoft 产品或下载之一：

+ [SQL Server 2017 机器学习服务](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 或更高版本](https://docs.microsoft.com/machine-learning-server/)
+ [数据科学客户端的 Python 客户端库](setup-python-client-tools-sql.md)

> [!NOTE]
> 完整的产品发布版本是 Windows 限、 从 SQL Server 2017 开始。 针对 Linux 支持**revoscalepy**中的新[SQL Server 2019 预览版](../../linux/sql-server-linux-setup-machine-learning.md)。

## <a name="functions-by-category"></a>按类别列出的函数

本节按类别，以便您了解如何使用每个列出的函数。 此外可以使用[目录](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)来按字母顺序查找函数。

## <a name="1-data-source-and-compute"></a>1-数据源和计算

**revoscalepy**包括用于创建数据源并将位置设置的函数或*计算上下文*，在其中执行计算。 下表列出了与 SQL Server 方案相关的函数。

SQL Server 和 Python 在某些情况下使用不同的数据类型。 有关 SQL 和 Python 的数据类型之间的映射的列表，请参阅[Python SQL 数据类型](python-libraries-and-data-types.md)。

| 函数| Description|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  创建将计算推送到远程实例的 SQL Server 计算上下文对象。 多个**revoscalepy**函数采用作为自变量的计算上下文。 有关上下文切换的示例，请参阅[使用 revoscalepy 创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)。|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | 创建基于 SQL Server 查询或表的数据对象。 |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| 创建基于 ODBC 连接的数据源。 |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | 创建基于本地 XDF 文件的数据源。 XDF 文件通常用于内存中将数据卸载到磁盘。 在使用更多的数据不是可以从一个批处理中的数据库传输或更多的数据多于可以容纳在内存中时，XDF 文件很有用。 例如，如果您定期大量数据从数据库移动到本地工作站，而不是查询重复的每个 R 操作，数据库可 XDF 文件作为缓存的一种保存数据保存在本地，然后使用它在 R 工作区中。 |

> [!TIP]
> 如果不熟悉的数据源的想法或计算上下文，我们建议您开始[分布式计算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)Microsoft Machine Learning Server 文档中。

## <a name="2-data-manipulation-etl"></a>2 数据操作 (ETL)

| 函数 | Description |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | 将数据导入.xdf 文件或数据帧。|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | 将数据从输入数据集中到一个输出数据集转换。|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 培训和摘要

| 函数| Description|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | 适合随机梯度提升的决策树|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | 适合分类和回归的决策林|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | 适合的分类和回归树 |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | 创建线性回归模型|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | 创建逻辑回归模型|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | 生成的单变量摘要 revoscalepy 中的对象。|

你还应查看中的函数[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)的其他方法。

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4 评分函数

| 函数| Description|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | 从训练的模型生成预测|) | 从训练的模型生成预测，并可用于进行实时评分。 |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | 计算预测的值，并使用 rx_lin_mod 和 rx_logit 对象的残差。 |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | 计算预测或条拟合的来自 rx_dforest 或 rx_btrees 对象的数据集的值。 |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | 计算预测或条拟合的来自 rx_dtree 对象的数据集的值。 |

## <a name="how-to-work-with-revoscalepy"></a>如何使用 revoscalepy

中的函数**revoscalepy**是可封装在存储过程的 Python 代码中调用。 大多数开发人员构建**revoscalepy**解决方案本地，然后将完成的 Python 代码作为部署练习迁移到存储过程。

本地运行时，通常要运行的 Python 脚本从命令行中，或从 Python 开发环境，并指定使用一个 SQL Server 计算上下文**revoscalepy**函数。 您可以使用远程计算上下文，对于整个代码中，或有关各个函数。 例如，你可能想要卸载到服务器以使用最新数据并避免数据移动的模型定型。

当你准备好将封装在存储过程，Python 脚本[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，我们建议为清晰地定义了输入和输出的单个函数重写代码。 

必须是输入和输出**pandas**数据帧。 完成此操作后，可以从支持 T-SQL 的任何客户端调用存储的过程、 轻松地传递 SQL 查询作为输入，并将结果保存到 SQL 表。 有关示例，请参阅[面向 SQL 开发人员了解数据库内 Python 分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)。

### <a name="using-revoscalepy-with-microsoftml"></a>Microsoftml 中使用 revoscalepy

为 Python 函数[microsoftml](ref-py-microsoftml.md) revoscalepy 中提供的计算上下文和数据源与集成在一起。 时从 microsoftml 调用函数，例如当定义和训练模型，使用 revoscalepy 函数执行 Python 本地代码或在 SQl Server 远程计算上下文。

下面的示例显示了导入 Python 代码中的模块的语法。 然后可以引用所需的各个函数。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>另请参阅

+ [Python 教程](../tutorials/sql-server-python-tutorials.md)
+ [教程：在 T-SQL 中嵌入 Python 代码](../tutorials/run-python-using-t-sql.md)
+ [Python 参考 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
