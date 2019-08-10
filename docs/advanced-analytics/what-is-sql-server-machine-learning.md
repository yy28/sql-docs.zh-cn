---
title: 什么是 SQL Server 机器学习服务 (Python 和 R)？
titleSuffix: ''
description: 机器学习服务是 SQL Server 中的一项功能, 它使你能够使用关系数据运行 Python 和 R 脚本。 你可以使用开源包和框架, 以及用于预测分析和机器学习的 Microsoft Python 和 R 包。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍了 SQL Server 机器学习服务的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 59e005e0075c9bb26210c6be9be5f52a3aa9a164
ms.sourcegitcommit: 3ec48823bee1c092ce2aba6011b95174de03fb65
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926915"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>什么是 SQL Server 机器学习服务 (Python 和 R)？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

机器学习服务是 SQL Server 中的一项功能, 它使你能够使用关系数据运行 Python 和 R 脚本。 你可以使用开源包和框架, 以及用于预测分析和机器学习的[Microsoft Python 和 R 包](#packages)。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍了 SQL Server 机器学习服务的基础知识。

在 Azure SQL 数据库中,[机器学习服务](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)当前为公共预览版。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 有关在 SQL Server 中执行 Java 的详细说明, 请参阅[语言扩展文档](../language-extensions/language-extensions-overview.md)。
::: moniker-end

## <a name="what-is-machine-learning-services"></a>什么是机器学习服务？

SQL Server 机器学习服务使你可以执行数据库中的 Python 和 R 脚本。 您可以使用它来准备和清理数据, 执行特征工程, 以及在数据库中训练、评估和部署机器学习模型。 此功能在数据所在的位置运行脚本, 并消除跨网络到另一台服务器的数据传输。

Python 和 R 的基本分发包含在机器学习服务中。 除了适用于 Python 的 Microsoft 包[revoscalepy](python/ref-py-revoscalepy.md)和[Microsoftml](python/ref-py-microsoftml.md) , 以及[RevoScaleR](r/ref-r-revoscaler.md)、 [microsoftml](r/ref-r-microsoftml.md)、 [olapR](r/ref-r-olapr.md)外, 还可以使用开源包和框架, 如 PyTorch、TensorFlow 和 scikit-learn。适用于 R 的[sqlrutils](r/ref-r-sqlrutils.md)和。

机器学习服务使用扩展性框架在 SQL Server 中运行 Python 和 R 脚本。 详细了解此功能的工作原理:

+ [扩展性框架](concepts/extensibility-framework.md)
+ [Python 扩展](concepts/extension-python.md)
+ [R 扩展](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>机器学习服务可以执行哪些操作？

您可以使用机器学习服务在 SQL Server 中生成和培训机器学习和深度学习模型。 您还可以将现有模型部署到机器学习服务, 并将关系数据用于预测。

可以使用 SQL Server 机器学习服务的预测类型的示例包括:

|||
|-|-|
|分类/分类|自动将客户反馈划分为正值和负值类别|
|回归/预测连续值|根据大小和位置预测房屋价格|
|异常检测|检测欺诈银行交易 |
|建议|根据客户以前购买的内容建议在线购物者可能希望购买的产品|

### <a name="how-to-execute-python-and-r-scripts"></a>如何执行 Python 和 R 脚本

可以通过两种方式在机器学习服务中执行 Python 和 R 脚本:

+ 最常见的方法是使用 T-sql 存储过程[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 你还可以使用首选的 Python 或 R 客户端并编写将执行 (称为*远程计算上下文*) 推送到远程 SQL Server 的脚本。 有关详细信息, 请参阅如何为[Python 开发](python/setup-python-client-tools-sql.md)和[R 开发](r/set-up-a-data-science-client.md)设置数据科学客户端。

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 和 R 包

除了 Microsoft 的企业包外, 还可以使用开源包和框架。 大多数常见的开源 Python 和 R 包都预安装在机器学习服务中。 还包括 Microsoft 提供的以下 Python 和 R 包:

| 语言 | package | 描述 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 可伸缩 Python 的主要包。 数据转换和操作、统计汇总、可视化和多种形式的建模。 此外, 此包中的函数会自动在可用内核之间分发工作负载, 以便进行并行处理。 |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 添加机器学习算法, 以便为文本分析、图像分析和情绪分析创建自定义模型。 | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 可缩放的 R 的主包。数据转换和操作、统计汇总、可视化和多种形式的建模。 此外, 此包中的函数会自动在可用内核之间分发工作负载, 以便进行并行处理。 |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | 添加机器学习算法, 以便为文本分析、图像分析和情绪分析创建自定义模型。 |
| R | [olapR](r/ref-r-olapr.md) | R 函数, 用于针对 SQL Server Analysis Services OLAP 多维数据集的 MDX 查询。 |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | 一种机制, 用于在 T-sql 存储过程中使用 R 脚本, 将该存储过程注册到数据库, 并从[R 开发环境](r/set-up-a-data-science-client.md)运行存储过程。 |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) 是 Microsoft 的增强版本。 它是一个用于统计分析和数据科学的完整开源平台。 它基于与 R 兼容的 100%, 并且包括更多的性能和可再现性的功能。 |

## <a name="how-do-i-get-started-with-machine-learning-services"></a>机器学习服务如何实现入门？

1. [安装 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)

1. 配置开发工具。 你可以使用:

    + [Azure Data Studio](../azure-data-studio/what-is.md)或[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md)使用 t-sql 和存储过程[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)执行 Python 或 R 脚本。
    + 你自己的开发便携式计算机或工作站上的 Python 或 R 来执行脚本。 可以在本地请求数据, 也可以远程推送执行, 以便 SQL Server [revoscalepy](python/ref-py-revoscalepy.md)和[RevoScaleR](r/ref-r-revoscaler.md)。 有关详细信息, 请参阅如何为[Python 开发](python/setup-python-client-tools-sql.md)和[R 开发](r/set-up-a-data-science-client.md)设置数据科学客户端。

1. 编写第一个 Python 或 R 脚本

    + 快速入门：[在 Python](tutorials/quickstart-python-run-using-t-sql.md)或[R 中](tutorials/quickstart-r-run-using-tsql.md)运行 "Hello world" 脚本
    + 快速入门：[在 Python](tutorials/quickstart-python-train-score-in-tsql.md)或[R 中](tutorials/quickstart-r-create-predictive-model.md)创建预测模型
    + 教程：[在 t-sql 中使用 Python](tutorials/sqldev-in-database-python-for-sql-developers.md):探索数据, 执行特征工程, 定型和部署模型, 并进行预测 (五部分系列)
    + 教程：[在 t-sql 中使用 R](tutorials/sqldev-in-database-r-for-sql-developers.md):探索数据, 执行特征工程, 定型和部署模型, 并进行预测 (五部分系列)
    + 教程：[使用 R 工具中的机器学习服务](tutorials/walkthrough-data-science-end-to-end-walkthrough.md):探索数据, 创建图形和绘图, 执行特征工程, 定型和部署模型, 并进行预测 (六部分系列)

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)
+ 为[Python 开发](python/setup-python-client-tools-sql.md)和[R 开发](r/set-up-a-data-science-client.md)设置数据科学客户端
