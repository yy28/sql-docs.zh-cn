---
title: 什么&#39;s SQL Server 机器学习服务中的新增功能 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf56d52823727609d713639d534e277be57caaef
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174804"
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>什么是 SQL Server 机器学习服务中的新增功能 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

机器学习功能添加到 SQL Server 每个版本中我们继续展开、 扩展和同时更深入的数据平台和数据科学，分析之间的集成和监督式的学习您想要实现对你的数据。 

## <a name="new-in-sql-server-2017"></a>SQL Server 2017 中的新增功能

此版本添加了 Python 支持和行业领先的机器学习算法。 重命名以反映新的作用域，SQL Server 2017 标记引入**SQL Server 机器学习服务 （数据库内）**，具有语言支持的 Python 和。 

此版本中还引入了**SQL Server 机器学习服务器 （独立版）**、 完全独立于 SQL Server，适用于你想要的专用系统上运行的 R 和 Python 工作负荷。 与独立服务器、 分发和缩放 R 或 Python 解决方案，而不使用 SQL Server。

| 发行版本 | 功能更新 |
|---------|----------------|
| CU 6 | Bug 修复和包刷新，但不是新特征的公告。 修补程序包括支持 DateTime 数据类型 SPEES 查询中为 Python 和 microsoftml 中的改进的错误消息缺少预先训练的模型时。 |
| CU 5 | Bug 修复和包刷新，但不是新特征的公告。 修复包括改进来转换函数并 revoscalepy，更正 rxInstallPackages，修复连接中环回 RxExec 和 rx_exec 函数和修订的警告消息，在长时间与路径相关的错误中的变量。 |
| CU 4 | Bug 修复和包刷新，但不是新特征的公告。 |
| CU 3 | Python 模型 revoscalepy 中的序列化使用[rx_serialize_model 函数](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/><br/>[本机计分](sql-native-scoring.md)plus 的增强功能[实时评分](real-time-scoring.md)。 与数据库中评分，吞吐量是 100 万行，每个使用 R 模型的第二个。 在此更新中，实时评分和本机计分提供更好的性能的单行和批处理评分。 本机计分使用快速评分的 T-SQL 函数可以在上运行任何版本的 SQL Server，即使在 Linux 上。 该函数不需要安装的 R 或额外的配置。 这意味着你可以训练的模型的其他位置，将其保存在 SQL Server，然后执行评分而不会调用。有关计分方法的详细信息，请参阅[如何执行实时评分或本机计分](r/how-to-do-realtime-scoring.md)。 |
| CU 2 | Bug 修复和包刷新，但不是新特征的公告。 |
| CU 1 | Revoscalepy，在将添加用于从 SQL Server 数据源，类似于返回架构信息 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)为。 <br/><br/>增强功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支持使用的并行方案`RxLocalParallel`计算上下文。|
| 初始版本 |[**数据库内分析的 Python 集成**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>[Revoscalepy](python/what-is-revoscalepy.md)包是 RevoScaleR 的 Python 的等效项。 可以创建用于线性回归和逻辑回归、 决策树、 提升的树和随机林，所有可并行化，并能够在远程计算上下文中正在运行的 Python 模型。 此包支持使用多个数据源和远程计算上下文。 在远程 SQL 服务器上，若要浏览数据或生成模型，而无需移动数据，数据科学家或开发人员可以执行 Python 代码。 <br/><br/>[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包是 MicrosoftML R 包的 Python 的等效项。<br/><br/>通过 T-SQL 和 Python 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 可以调用任何使用此存储的过程的 Python 代码。 此安全的基础结构支持企业级部署 Python 模型和可以从应用程序使用的简单存储的过程调用的脚本。 是通过将数据从 SQL 流式处理到 Python 进程和 MPI 环并行化来实现更多的性能提升。 <br/><br/>可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函数来执行[本机计分](sql-native-scoring.md)上具有所需的二进制格式中的以前保存的预先训练模型。|
| 初始版本 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md)包含先进的机器学习算法和数据可以是缩放或运行在远程计算上下文的转换。 算法包括可自定义的深度神经网络、 快速决策树和决策林、 线性回归和逻辑回归。 |
| 初始版本 | [**预先训练的模型**](install/sql-pretrained-models-install.md)图像识别和正负情绪分析。 使用这些模型来生成你自己的数据的预测。 |
| 初始版本 | [**R 包管理**](r/install-additional-r-packages-on-sql-server.md)，包括以下突出显示部分： 数据库角色，以帮助管理包和分配权限来安装包，DBA [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)中到 T-SQL 语句帮助 Dba 管理包而无需了解 R、 和中的一组丰富的 R 函数[RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)来帮助安装、 删除或列出包所拥有的用户。 |
| 初始版本 | [**操作化通过 mrsdeploy** ](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)用于部署和托管作为 web 服务的 R 脚本。 适用于仅限用于 R 脚本 （没有 Python 等效项）。 适用于 （独立版） 的服务器选项，以避免与其他 SQL Server 操作的资源竞争。 |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016 中的新增功能

此发行版引入了机器学习的功能到通过 SQL Server **SQL Server 2016 R Services**，数据库引擎实例中的常驻数据处理 R 脚本在数据库中分析引擎。

此外， **SQL Server 2016 R Server （独立版）** 作为一种方式在 Windows 服务器上安装 R Server 发布。 最初，SQL Server 安装程序提供安装 R Server 的 Windows 的唯一方法。 在更高版本中，开发人员和想要在 Windows 上的 R Server 的数据科学家可以使用另一个独立安装程序来完成相同的目标。 SQL Server 中的独立服务器在功能上等效于独立服务器产品来说[Microsoft R Server 的 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

| 发行版本 |功能更新 |
|---------|----------------|
| CU 的新增功能 | [**实时评分**](real-time-scoring.md)依赖于本机 c + + 库读取模型中优化的二进制格式，存储，而无需调用 R 运行时来生成预测。 这使得计分操作要快得多。 使用实时评分，可以运行存储的过程或执行实时评分从 R 代码。 也可用于 SQL Server 2016 中，如果该实例升级到最新版本的实时评分是[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 初始版本 | [**数据库内分析的 R 集成**](r/sql-server-r-services.md)。 <br/><br/> 调用 R 的 R 包的函数在 T-SQL，反之亦然。 RevoScaleR 函数提供大规模的 R 分析通过对数据进行分块成组件部分，协调和管理分布式处理和聚合结果。 在 SQL Server 2016 R Services （数据库内），RevoScaleR 引擎集成使用数据库引擎实例，善于数据和分析组合在一起的处理上下文中。 <br/><br/>通过 T-SQL 和 R 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 可以调用使用此存储的过程的任何 R 代码。 此安全的基础结构支持企业级部署 Rn 模型和可以从应用程序使用的简单存储的过程调用的脚本。 是通过将数据从 SQL 流式处理到 R 进程和 MPI 环并行化来实现更多的性能提升。 <br/><br/>可以使用 T-SQL [PREDICT](../t-sql/queries/predict-transact-sql.md)函数来执行[本机计分](sql-native-scoring.md)上具有所需的二进制格式中的以前保存的预先训练模型。|

## <a name="linux-support-roadmap"></a>Linux 支持路线图

机器学习中使用 R 或 Python 中的数据库当前不支持在 Linux 上的 SQL Server 中。 查看我们的更高版本中的通知。

但是，在 Linux 上可以执行[本机计分](sql-native-scoring.md)使用 T-SQL 的预测函数。 本机计分，可以从预先训练的模型非常快，评分而无需调用或甚至要求 R 运行时。 这意味着可以使用在 Linux 上的 SQL Server 来生成预测非常快，若要为客户端应用程序服务。

<a name="azure-sql-database-roadmap"></a>

## <a name="azure-sql-database-roadmap"></a>Azure SQL 数据库路线图

Azure SQL 数据库中的 R 的有限支持： 仅在美国中西部，在高级层创建的服务中可用。 扩展服务范围，其中包括 Python 支持，很可能在将来的版本中遵循。 但是，这一次出现是没有预计的发行日期。  

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 2017 机器学习服务 （数据库内）](install/sql-machine-learning-services-windows-install.md)
+ [机器学习教程和示例](tutorials/machine-learning-services-tutorials.md)
