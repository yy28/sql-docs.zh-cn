---
title: 什么&#39;s 新的 SQL Server 机器学习服务
description: 新的 SQL Server 2016 R Services、 R Server、 SQL Server 2017 机器学习服务的每个版本的功能公告。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f9e98d59318c9c7d43fd6f99195da972c4eca0c9
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432490"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>什么是 SQL Server 机器学习服务中的新增功能 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

机器学习功能将添加到 SQL Server 中每个版本，随着我们继续展开、 扩展和强化数据平台、 高级的分析和数据科学之间的集成。 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2019-preview"></a>SQL Server 2019 预览版中的新增功能

此版本添加了 SQL Server 中 R 和 Python 机器学习操作的请求频率最高的功能。 有关此版本中功能的所有详细信息，请参阅[What's New in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)并[Release Notes for SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md)。

| 发行版本 | 功能更新 |
|---------|----------------|
| CTP 2.0 | R 和 Python 机器学习的 Linux 平台支持。 开始使用[安装 SQL Server 机器学习服务在 Linux 上](../linux/sql-server-linux-setup-machine-learning.md)。 |
|   | [Java 语言扩展](java/extension-java.md)Windows 和 Linux 上为 SQL Server 2019 预览版中的新增功能。 您可以提供编译的 Java 代码到 SQL Server 通过将权限分配并将路径设置。 使用 SQL Server 的访问权限的客户端应用程序可以使用数据并运行你的代码通过调用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，相同的过程用于 SQL Server 上的 R 和 Python 集成。 | 
|  | [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)引入了使你能够轻松地从已分区数据中生成多个模型的两个新参数。 在本教程中，了解详细信息[在 R 中创建基于分区的模型](tutorials/r-tutorial-create-models-per-partition.md)。 |
|   | 故障转移群集支持现在支持 Windows 和 Linux，假定所有节点上启动 SQL Server Launchpad 服务。 有关详细信息，请参阅[SQL Server 故障转移群集安装](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)。 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="new-in-sql-server-2017"></a>SQL Server 2017 中的新增功能

此版本添加了[的 Python 支持和行业领先的机器学习算法](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)。 重命名以反映新的作用域，SQL Server 2017 标记引入[SQL Server 机器学习服务 （数据库内）](what-is-sql-server-machine-learning.md)，具有语言支持的 Python 和。 

有关功能的公告大幅度，请参阅[What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。

### <a name="r-enhancements"></a>R 的增强功能

SQL Server 2017 机器学习服务的 R 组件是 SQL Server 2016 R Services 下, 一代基础 R、 RevoScaler 和其他包的更新版本。

适用于 R 的新功能包括[**包管理**](r/install-additional-r-packages-on-sql-server.md)，具有如下要点： 

+ 数据库角色可帮助 Dba 管理包和包安装为分配权限。
+ [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)帮助 Dba 管理中熟悉的 T-SQL 语言包。
+ [RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)函数帮助安装，由用户拥有删除或列出的包。 有关详细信息，请参阅[如何使用 RevoScaleR 函数来查找或安装 R 包的 SQL Server 上](r/use-revoscaler-to-manage-r-packages.md)。

### <a name="r-libraries"></a>R 库

| package | Description |
|---------|-------------|
| [**MicrosoftML**](r/ref-r-microsoftml.md) | 在此版本中，MicrosoftML 包含在默认 R 安装中，消除了以前的 SQL Server 2016 R Services 中所需的升级步骤。 MicrosoftML 提供最先进的机器学习算法和数据转换，可进行缩放或在远程计算上下文中运行。 算法包括可自定义的深度神经网络、 快速决策树和决策林、 线性回归和逻辑回归。  |

### <a name="python-integration-for-in-database-analytics"></a>数据库内分析的 Python 集成

Python 是一种语言，提供了极大的灵活性和各种机器学习任务的能力。 用于 Python 的开放源代码库包括多个平台的可自定义神经网络，以及进行自然语言处理的常用库。 现在，在 SQL Server 2017 机器学习中支持此广泛使用的语言。

由于 Python 集成了数据库引擎，可以让分析贴近数据，并消除成本和与数据移动相关的安全风险。 你可以部署基于 Python 使用 Visual Studio 等工具的机器学习解决方案。 对生产应用程序可以获取预测模型，或视觉对象从 Python 3.5 运行时使用 SQL Server 数据访问方法。

通过支持 T-SQL 和 Python 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系统存储过程。 可以调用任何使用此存储的过程的 Python 代码。 在安全的双向体系结构，使企业级部署 Python 模型和脚本，可从应用程序使用的简单存储的过程调用中运行代码。 是通过将数据从 SQL 流式处理到 Python 进程和 MPI 环并行化来实现更多的性能提升。

可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函数来执行[本机计分](sql-native-scoring.md)上具有所需的二进制格式中的以前保存的预先训练模型。

### <a name="python-libraries"></a>Python 库

| package | Description |
|---------|-------------|
[**revoscalepy**](python/ref-py-revoscalepy.md)| Python 等效于 RevoScaleR。 可以创建用于线性回归和逻辑回归、 决策树、 提升的树和随机林，所有可并行化，并能够在远程计算上下文中正在运行的 Python 模型。 此包支持使用多个数据源和远程计算上下文。 在远程 SQL 服务器上，若要浏览数据或生成模型，而无需移动数据，数据科学家或开发人员可以执行 Python 代码。 |
|[**microsoftml**](python/ref-py-microsoftml.md) |MicrosoftML R 包的 Python 等效。 |

### <a name="pre-trained-models"></a>预定型模型

[**预先训练的模型**](install/sql-pretrained-models-install.md)了可用于 Python 和。 使用这些模型进行图像识别和正负情绪分析，以生成在你自己的数据的预测。 

### <a name="standalone-server-as-a-shared-feature-in-sql-server-setup"></a>作为共享功能在 SQL Server 安装程序的独立服务器

此版本还添加了[SQL Server 机器学习服务器 （独立版）](r/r-server-standalone.md)，支持 R 和 Python 中的统计和预测分析的完全独立的数据科学服务器。 作为使用 R Services，此服务器是 SQL Server 2016 R Server （独立版） 的下一版本。 与独立服务器、 分发和缩放 SQL Server 上的 R 或 Python 解决方案没有依赖项。
::: moniker-end

## <a name="new-in-sql-server-2016"></a>SQL Server 2016 中的新增功能

此发行版引入了机器学习的功能到通过 SQL Server **SQL Server 2016 R Services**，数据库引擎实例中的常驻数据处理 R 脚本在数据库中分析引擎。

此外， **SQL Server 2016 R Server （独立版）** 作为一种方式在 Windows 服务器上安装 R Server 发布。 最初，SQL Server 安装程序提供安装 R Server 的 Windows 的唯一方法。 在更高版本中，开发人员和想要在 Windows 上的 R Server 的数据科学家可以使用另一个独立安装程序来完成相同的目标。 SQL Server 中的独立服务器在功能上等效于独立服务器产品来说[Microsoft R Server 的 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

有关功能的公告大幅度，请参阅[What's New in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)。

| 发行版本 |功能更新 |
|---------|----------------|
| CU 的新增功能 | [**实时评分**](real-time-scoring.md)依赖于本机 c + + 库读取模型中优化的二进制格式，存储，而无需调用 R 运行时来生成预测。 这使得计分操作要快得多。 使用实时评分，可以运行存储的过程或执行实时评分，从 R 代码。 也可用于 SQL Server 2016 中，如果该实例升级到最新版本的实时评分是[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 初始版本 | [**数据库内分析的 R 集成**](r/sql-server-r-services.md)。 <br/><br/> 调用 R 的 R 包的函数在 T-SQL，反之亦然。 RevoScaleR 函数提供大规模的 R 分析通过对数据进行分块成组件部分，协调和管理分布式处理和聚合结果。 在 SQL Server 2016 R Services （数据库内），RevoScaleR 引擎集成使用数据库引擎实例，善于数据和分析组合在一起的处理上下文中。 <br/><br/>通过 T-SQL 和 R 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 可以调用使用此存储的过程的任何 R 代码。 此安全的基础结构支持企业级部署 Rn 模型和可以从应用程序使用的简单存储的过程调用的脚本。 是通过将数据从 SQL 流式处理到 R 进程和 MPI 环并行化来实现更多的性能提升。 <br/><br/>可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函数来执行[本机计分](sql-native-scoring.md)上具有所需的二进制格式中的以前保存的预先训练模型。|

## <a name="linux-support-roadmap"></a>Linux 支持路线图

安装机器学习使用数据库引擎实例的包时，SQL Server 2019 CTP 2.0 添加 R、 Python 和 Java 的 Linux 支持。 有关详细信息，请参阅[安装 SQL Server 机器学习服务在 Linux 上](../linux/sql-server-linux-setup-machine-learning.md)。

在 Linux 上，SQL Server 2017 没有 R 或 Python 集成，但可以使用[本机计分](sql-native-scoring.md)Linux 上因为该功能是可通过 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)，在 Linux 上运行。 本机计分，从预先训练的模型，评分而无需调用或甚至要求 R 运行时的高性能。

<a name="azure-sql-database-roadmap"></a>

## <a name="machine-learning-services-in-azure-sql-database"></a>Azure SQL 数据库中机器学习服务

机器学习服务 （使用 R) Azure SQL 数据库中处于公共预览状态。 有关详细信息，请参阅[快速入门：在 Azure SQL 数据库 （预览版） 中使用机器学习服务 （使用 R)](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-r)。

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 2017 机器学习服务 （数据库内）](install/sql-machine-learning-services-windows-install.md)
+ [机器学习教程和示例](tutorials/machine-learning-services-tutorials.md)
