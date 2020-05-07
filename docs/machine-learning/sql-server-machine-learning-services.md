---
title: 什么是 SQL Server 机器学习服务（Python 和 R）？
titleSuffix: ''
description: 机器学习服务是 SQL Server 中一项支持使用关系数据运行 Python 和 R 脚本的功能。 可以使用开源包和框架，以及 Microsoft Python 和 R 包进行预测分析和机器学习。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍 SQL Server 机器学习服务的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/06/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: afce689bffe69de78970006aea51ddd49481e614
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220652"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>什么是 SQL Server 机器学习服务（Python 和 R）？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

机器学习服务是 SQL Server 中一项支持使用关系数据运行 Python 和 R 脚本的功能。 可以使用开源包和框架，以及 [Microsoft Python 和 R 包](#packages)进行预测分析和机器学习。 脚本在数据库中执行，而不将数据移动到 SQL Server 外部或是在网络上移动。 本文介绍 SQL Server 机器学习服务的基础知识。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 要在 SQL Server 中执行 Java，请参阅[语言扩展文档](../language-extensions/language-extensions-overview.md)。
::: moniker-end

## <a name="what-is-machine-learning-services"></a>什么是机器学习服务？

使用 SQL Server 机器学习服务，你可以在数据库中执行 Python 和 R 脚本。 可以使用它来准备和清理数据、执行特征工程以及在数据库中定型、评估和部署机器学习模型。 此功能在数据所在的位置运行脚本，无需通过网络将数据传输到其他服务器。

Python 和 R 的基本分发包含在机器学习服务中。 除了用于 Python 的 [revoscalepy](python/ref-py-revoscalepy.md) 和 [microsoftml](python/ref-py-microsoftml.md) Microsoft 包，以及用于 R 的 [RevoScaleR](r/ref-r-revoscaler.md)、[MicrosoftML](r/ref-r-microsoftml.md)、[olapR](r/ref-r-olapr.md) 和 [sqlrutils](r/ref-r-sqlrutils.md) 外，还可以安装和使用开源包和框架，如 PyTorch、TensorFlow 和 scikit-learn。

机器学习服务使用扩展性框架在 SQL Server 中运行 Python 和 R 脚本。 详细了解工作原理：

+ [扩展性框架](concepts/extensibility-framework.md)
+ [Python 扩展](concepts/extension-python.md)
+ [R 扩展](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>机器学习服务可以用于执行哪些操作？

可以使用机器学习服务在 SQL Server 中生成和定型机器学习和深度学习模型。 还可以将现有模型部署到机器学习服务，并使用关系数据进行预测。

以下为可以使用 SQL Server 机器学习服务进行的预测的示例类型：

|||
|-|-|
|分类/类别|自动将客户反馈分为积极和消极两类|
|回归/预测连续值|根据面积和地段预测房价|
|异常检测|检测欺诈性的银行交易 |
|建议|根据网购者以前的购买情况，推荐他们可能想购买的产品|

### <a name="how-to-execute-python-and-r-scripts"></a>如何执行 Python 和 R 脚本

在机器学习服务中有两种执行 Python 和 R 脚本的方法：

+ 最常见的方法是使用 T-SQL 存储过程 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 还可以使用首选的 Python 或 R 客户端并编写将执行（称为“远程计算上下文”）推送到远程 SQL Server 的脚本  。 有关详细信息，请参阅如何为 [Python 开发](python/setup-python-client-tools-sql.md)和 [R 开发](r/set-up-a-data-science-client.md)设置数据科学客户端。

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Python 和 R 版本

下面列出每个 SQL Server 版本的机器学习服务中包含的 Python 和 R 版本。

| SQL Server 版本 | Python 版本 | R 版本 |
|-|-|-|
| SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

有关 SQL Server 2016 中的 R 版本，请参阅[“什么是 R 服务？”中的“R 版本”部分](r/sql-server-r-services.md#version)

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 和 R 包

除了 Microsoft 的企业包外，还可以使用开源包和框架。 大多数常见的开源 Python 和 R 包都已预装在机器学习服务中。 还包括 Microsoft 提供的以下 Python 和 R 包：

| 语言 | 程序包 | 说明 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 可缩放的 Python 的主包。 数据转换和操作、统计摘要、可视化和多种形式的建模。 此外，此包中的函数会自动在可用内核之间分配工作负载以进行并行处理。 |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 添加机器学习算法，以便为文本分析、图像分析和情绪分析创建自定义模型。 | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 用于可缩放 R 的主包。数据转换和操作、统计摘要、可视化和多种形式的建模。 此外，此包中的函数会自动在可用内核之间分配工作负载以进行并行处理。 |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | 添加机器学习算法，以便为文本分析、图像分析和情绪分析创建自定义模型。 |
| R | [olapR](r/ref-r-olapr.md) | R 函数，用于针对 SQL Server Analysis Services OLAP 多维数据集进行 MDX 查询。 |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | 一种在 T-SQL 存储过程中使用 R 脚本、将该存储过程注册到数据库并在 [R 开发环境](r/set-up-a-data-science-client.md)中运行存储过程的机制。 |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) 是 Microsoft 中 R 的增强型分发。 它是用于统计分析和数据科学的完整开源平台。 它基于 R，并 100% 与 R 兼容，包括很多其他功能，可以带来更高的性能和可再现性。 |

有关与机器学习服务一并安装的包以及如何安装其他包的详细信息，请参阅：

+ [获取 Python 包信息](package-management/python-package-information.md)
+ [使用 sqlmlutils 安装 Python 包](package-management/install-additional-python-packages-on-sql-server.md)
+ [获取 R 包信息](package-management/r-package-information.md)
+ [使用 sqlmlutils 安装 新的 R 包](package-management/install-additional-r-packages-on-sql-server.md)。

## <a name="how-do-i-get-started-with-machine-learning-services"></a>如何开始使用机器学习服务入门？

1. [安装 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)

1. 配置开发工具。 可用工具如下：

    + 通过 [Azure Data Studio](../azure-data-studio/what-is.md) 或 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 来使用 T-SQL 和存储过程 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 执行 Python 或 R 脚本。
    + 在自己的开发便携式计算机或工作站上使用 Python 或 R 来执行脚本。 你可以在本地请求数据，也可以使用 [revoscalepy](python/ref-py-revoscalepy.md) 和 [RevoScaleR](r/ref-r-revoscaler.md) 将执行远程推送到 SQL Server。 有关详细信息，请参阅如何为 [Python 开发](python/setup-python-client-tools-sql.md)和 [R 开发](r/set-up-a-data-science-client.md)设置数据科学客户端。

1. 编写你的第一个 Python 或 R 脚本

    + 快速入门：[运行简单的 Python 脚本](tutorials/quickstart-python-create-script.md)
    + 快速入门：[运行简单的 R 脚本](tutorials/quickstart-r-create-script.md)
    + 教程：[在 T-SQL 中使用 Python](tutorials/sqldev-in-database-python-for-sql-developers.md)：探索数据、执行特征工程、定型和部署模型，并进行预测（五部分构成的系列）
    + 教程：[在 T-SQL 中使用 R](tutorials/sqldev-in-database-r-for-sql-developers.md)：探索数据、执行特征工程、定型和部署模型，并进行预测（五部分构成的系列）

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)
+ 设置用于 [Python 开发](python/setup-python-client-tools-sql.md)和 [R 开发](r/set-up-a-data-science-client.md)的数据科学客户端
