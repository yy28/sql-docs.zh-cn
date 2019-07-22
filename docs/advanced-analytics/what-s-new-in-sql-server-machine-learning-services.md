---
title: 新增功能 |Microsoft Docs
description: 适用于每个版本的 SQL Server 2016 R Services、R Server SQL Server 2017 机器学习服务的每个版本的新功能公告。
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 0e3859cfb1ada6453a353509b68abe34e71d2840
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345777"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>SQL Server 中的新增功能机器学习服务

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

将机器学习功能添加到每个版本的 SQL Server, 因为我们将继续扩展、扩展和加深数据平台、高级分析和数据科学之间的集成。 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>2019 SQL Server 中的新增预览版

此版本在 SQL Server 中添加 R 和 Python 机器学习操作的顶级请求功能。 有关此版本中所有功能的详细信息, 请参阅 SQL Server 2019 [SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)和[发行说明](../sql-server/sql-server-ver15-release-notes.md)中的新增功能。

> [!NOTE]
> 有关 SQL Server 2019 中 Java 的新增功能文档, 请参阅[SQL Server 语言扩展中的新增功能？](https://docs.microsoft.com/sql/language-extensions/language-extensions-whats-new)

| 发行版本 | 功能更新 |
|---------|----------------|
| CTP 3.0 | 无更改。 |
| CTP 2.5 | 无更改。 |
| CTP 2.4 | Linux 支持创建适用于 R 和 Python 的[外部库 (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md) 。 |
| CTP 2.3 | 仅在 Windows 上, 可使用[CREATE EXTERNAL library (transact-sql)](../t-sql/statements/create-external-library-transact-sql.md)语句在外部库中访问 Python 代码。 |
| CTP 2.2 | 无更改。 |
| CTP 2.1 | 无更改。 |
| CTP 2.0 | 适用于 R 和 Python 机器学习的 Linux 平台支持。 开始[在 Linux 上安装 SQL Server 机器学习服务](../linux/sql-server-linux-setup-machine-learning.md)。 |
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)引入了两个新参数, 可让你轻松地从分区数据生成多个模型。 有关详细信息, 请参阅本教程中的在[R 中创建基于分区的模型](tutorials/r-tutorial-create-models-per-partition.md)。 |
|   | Windows 和 Linux 现在支持故障转移群集支持, 前提是在所有节点上启动 SQL Server Launchpad 服务。 有关详细信息, 请参阅[SQL Server 故障转移群集安装](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)。 |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017 中的新增项

此版本添加了[Python 支持和行业领先的机器学习算法](https://cloudblogs.microsoft.com/sqlserver/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)。 重命名以反映新的作用域, SQL Server 2017 [SQL Server 机器学习服务 (数据库内)](what-is-sql-server-machine-learning.md)的引入, 同时提供 Python 和 R 的语言支持。 

有关功能公告的全部功能, 请参阅[SQL Server 2017 中的新增](../sql-server/what-s-new-in-sql-server-2017.md)功能。

### <a name="r-enhancements"></a>R 增强功能

SQL Server 2017 机器学习服务的 R 组件是下一代 SQL Server 2016 R 服务, 其中包含基本 R、RevoScaler 和其他包的更新版本。

适用于 R 的新功能包括[**包管理**](r/install-additional-r-packages-on-sql-server.md), 其中突出显示了以下内容: 

+ 数据库角色可帮助 Dba 管理包, 并为包安装分配权限。
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)有助于 dba 以熟悉的 t-sql 语言管理包。
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)函数可帮助安装、删除或列出用户拥有的包。 有关详细信息, 请参阅[如何使用 RevoScaleR 函数在 SQL Server 上查找或安装 R 包](r/use-revoscaler-to-manage-r-packages.md)。

### <a name="r-libraries"></a>R 库

| package | 描述 |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 在此版本中, MicrosoftML 包括在默认 R 安装中, 从而消除了之前 SQL Server 2016 R Services 中所需的升级步骤。 MicrosoftML 提供先进的机器学习算法和可在远程计算上下文中运行的数据转换。 算法包括可自定义的深层神经网络、快速决策树和决策林、线性回归和逻辑回归。  |

### <a name="python-integration-for-in-database-analytics"></a>用于数据库内分析的 Python 集成

Python 是一种语言, 可为各种机器学习任务提供极大的灵活性和强大功能。 用于 Python 的开源库包括可自定义的神经网络的多个平台以及用于自然语言处理的常用库。 现在, SQL Server 2017 机器学习支持这种广泛使用的语言。

由于 Python 与数据库引擎集成, 你可以保持与数据接近的分析, 消除与数据移动相关的成本和安全风险。 你可以使用 Visual Studio 之类的工具基于 Python 部署机器学习解决方案。 使用 SQL Server 数据访问方法, 生产应用程序可以从 Python 3.5 运行时获取预测、模型或视觉对象。

通过[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储过程支持 T-sql 和 Python 集成。 您可以使用此存储过程调用任何 Python 代码。 代码在安全的双体系结构中运行, 该体系结构允许企业级部署 Python 模型和脚本, 并使用简单的存储过程从应用程序中调用。 通过从 SQL 到 Python 进程和 MPI 环形并行处理数据, 实现更多性能提升。

您可以使用 T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)函数对之前以所需二进制格式保存的预先训练的模型执行[本机评分](sql-native-scoring.md)。

### <a name="python-libraries"></a>Python 库

| package | 描述 |
|---------|-------------|
|[**revoscalepy**](python/ref-py-revoscalepy.md)| Python-等效于 RevoScaleR。 您可以为线性和逻辑回归、决策树、提升树和随机林创建 Python 模型, 所有可并行化, 并能够在远程计算上下文中运行。 此包支持使用多个数据源和远程计算上下文。 数据科研人员或开发人员可以在远程 SQL Server 上执行 Python 代码, 以浏览数据或生成模型, 而无需移动数据。 |
|[**microsoftml**](python/ref-py-microsoftml.md) |Python-等效于 MicrosoftML R 包。 |

### <a name="pre-trained-models"></a>预定型模型

[**预先训练的模型**](install/sql-pretrained-models-install.md)可用于 Python 和 R。将这些模型用于图像识别和正负情绪分析, 以便根据自己的数据生成预测。 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>独立服务器作为 SQL Server 安装程序中的共享功能

此版本还添加了[SQL Server Machine Learning Server (独立)](r/r-server-standalone.md), 这是一个完全独立的数据科学服务器, 支持 R 和 Python 中的统计分析和预测分析。 对于 R 服务, 此服务器是 SQL Server 2016 R Server (独立版) 的下一版本。 对于独立服务器, 你可以分发和缩放 R 或 Python 解决方案, 但不依赖于 SQL Server。
::: moniker-end

## <a name="new-in-sql-server-2016"></a>SQL Server 2016 中的新增项

此版本引入了机器学习功能 SQL Server 通过**SQL Server 2016 R 服务**, 这是一个数据库内分析引擎, 用于处理数据库引擎实例中驻留数据的 R 脚本。

此外, **SQL Server 2016 R server (独立版)** 已发布为在 Windows Server 上安装 R server 的一种方法。 最初, SQL Server 安装程序提供了安装 R Server for Windows 的唯一方法。 在更高版本中, 希望 R Server on Windows 的开发人员和数据科学家可以使用另一个独立的安装程序实现相同的目标。 SQL Server 中的独立服务器在功能上等同于[适用于 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)的独立服务器产品 Microsoft R Server。

有关功能公告的全部功能, 请参阅[SQL Server 2016 中的新增](../sql-server/what-s-new-in-sql-server-2016.md)功能。

| 发行版本 |功能更新 |
|---------|----------------|
| CU 添加 | [**实时评分**](real-time-scoring.md)依赖于本机C++库来读取以优化二进制格式存储的模型, 然后生成预测, 而不必调用 R 运行时。 这使得评分操作的速度更快。 使用实时评分, 你可以运行存储过程或执行 R 代码的实时评分。 如果实例升级到的[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]最新版本, 则还可用于 SQL Server 2016 的实时评分。 |
| 初始版本 | [**用于数据库内分析的 R 集成**](r/sql-server-r-services.md)。 <br/><br/> 用于在 T-sql 中调用 R 函数的 r 包, 反之亦然。 RevoScaleR 函数通过将数据分块到组件部分、协调和管理分布式处理以及聚合结果, 大规模提供 R analytics。 在 SQL Server 2016 R Services (数据库内) 中, RevoScaleR 引擎与数据库引擎实例集成在一起, 并在相同的处理上下文中 brining 数据和分析。 <br/><br/>T-sql 和 R 与[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)的集成。 您可以使用此存储过程调用任何 R 代码。 利用此安全基础结构, 可以使用简单的存储过程通过应用程序调用 Rn 模型和脚本的企业级部署。 通过从 SQL 到 R 进程和 MPI 环形并行处理数据, 实现更高的性能提升。 <br/><br/>您可以使用 T-sql [PREDICT](../t-sql/queries/predict-transact-sql.md)函数对之前以所需二进制格式保存的预先训练的模型执行[本机评分](sql-native-scoring.md)。|

## <a name="linux-support-roadmap"></a>Linux 支持路线图

SQL Server 2019 CTP 2.3 在使用数据库引擎实例安装机器学习包时添加了适用于 R 和 Python 的 Linux 支持。 有关详细信息, 请参阅[在 Linux 上安装 SQL Server 机器学习服务](../linux/sql-server-linux-setup-machine-learning.md)。

在 Linux 上, SQL Server 2017 没有 R 或 Python 集成, 但你可以使用 Linux 上的[本机计分](sql-native-scoring.md), 因为该功能可通过 t-sql[预测](../t-sql/queries/predict-transact-sql.md)(在 linux 上运行) 提供。 本机计分实现预先训练模型的高性能计分, 无需调用, 甚至无需调用 R 运行时。

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>在 Azure SQL 数据库中机器学习服务

Azure SQL 数据库中的机器学习服务 (R) 是公共预览。 有关详细信息, 请参阅[AZURE SQL Database 机器学习服务 With R (预览版)](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)。

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 2017 机器学习服务 (数据库内)](install/sql-machine-learning-services-windows-install.md)
+ [机器学习教程和示例](tutorials/machine-learning-services-tutorials.md)
