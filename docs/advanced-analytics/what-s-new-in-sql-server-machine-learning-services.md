---
title: 什么&#39;SQL Server 计算机学习 Services 中的新增功能 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0f0487d26e602504fc776b1262414488e24c8336
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="whats-new-in-sql-server-machine-learning-services"></a>什么是 SQL Server 计算机学习 Services 中的新增功能 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

机器学习功能将添加到 SQL Server 中每个版本随着我们继续展开、 扩展和深化数据平台和数据科学，分析，之间的集成和监督的学习想要实现针对您的数据。 

## <a name="new-in-sql-server-2017"></a>SQL Server 自 2017 年中的新增功能

此版本添加 Python 支持和行业领先的机器学习算法。 重命名以反映新作用域，SQL Server 2017 标记的简介**SQL Server 计算机学习 Services （数据库）**，语言支持 Python 和。 

此发行版还引入了**SQL Server 计算机学习服务器 （独立）**完全独立于 SQL Server，对于你想要的专用系统上运行的 R 和 Python 的工作负荷。 与独立服务器，您可以分发，而无需使用 SQL Server 扩展 R 或 Python 的解决方案。

| 发行版本 | 功能更新 |
|---------|---------------|
| CU 4 | Bug 修复程序和包刷新，但不是新的功能公告。 |
| CU 3 | Python 模型 revoscalepy 中的序列化使用[rx_serialize_model 函数](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/><br/>[本机评分](sql-native-scoring.md)plus 的增强功能[实时评分](real-time-scoring.md)。 与数据库中评分，吞吐量是基于每 100 万行倒数第二次使用 R 模型。 在此更新中，实时评分和本机评分提供更好的性能单行更行和批处理评分。 本机评分使用快速评分的 T-SQL 的函数可以运行在任何版本的 SQL Server，即使在 Linux 上。 该函数不需要安装的 R 或额外的配置。 这意味着你可以训练模型在其他位置，将其保存在 SQL Server，然后执行评分而不会调用。计分方法的详细信息，请参阅[如何执行实时评分或本机评分](r/how-to-do-realtime-scoring.md)。 |
| CU 2 | Bug 修复程序和包刷新，但不是新的功能公告。 |
| CU 1 | 在 revoscalepy，添加用于从 SQL Server 数据源，类似于返回架构信息 rx_create_col_info [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo)为。 <br/><br/>增强功能[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支持使用的并行方案`RxLocalParallel`计算上下文。|
| 初始版本 |[**数据库中分析的 Python 集成**](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/) <br/><br/>[Revoscalepy](python/what-is-revoscalepy.md)包是 RevoScaleR 的 Python 等效项。 你可以创建用于线性和逻辑回归、 决策树，提升的树和随机林，所有可并行化，并且能够在远程计算上下文中运行的 Python 模型。 此包支持使用多个数据源和远程计算上下文。 在远程 SQL 服务器上，若要浏览数据或生成模型，而无需移动数据，数据科研人员或开发人员可以执行 Python 代码。 <br/><br/>[Microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包是 MicrosoftML R 包的 Python 等效项。<br/><br/>通过的 T-SQL 和 Python 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 你可以调用任何使用此存储的过程的 Python 代码。 此安全基础结构支持 Python 模型和脚本，可以从使用简单的存储的过程的应用程序调用的企业级部署。 可通过从 SQL Python 进程和 MPI 环并行化的流式处理数据来实现更多的性能提升。 <br/><br/>你可以使用 T-SQL 的[预测](../t-sql/queries/predict-transact-sql.md)函数来执行[本机评分](sql-native-scoring.md)上预先训练的模型已以前保存在所需的二进制格式。|
| 初始版本 | [**MicrosoftML (R)** ](using-the-microsoftml-package.md)包含最先进的机器学习算法和数据可以是缩放或运行在远程计算上下文的转换。 算法包括可自定义深层神经网络、 快速决策树和决策林、 线性回归和逻辑回归。 |
| 初始版本 | [**预先训练的模型**](r/install-pretrained-models-sql-server.md)图像识别和正负观点分析。 使用这些模型来生成在你自己的数据的预测。 |
| 初始版本 | [**包管理**](r/r-package-management-for-sql-server-r-services.md)，包括以下突出显示： 数据库角色，以帮助 DBA 管理包和分配权限以安装程序包[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)中到 T-SQL 语句帮助 Dba 管理包而无需知道 R，和一组丰富的 R 函数中[RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)来帮助安装、 删除或列出程序包拥有的用户。 |
| 初始版本 | [**通过 mrsdeploy 操作化**](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)用于部署和托管作为 web 服务的 R 脚本。 适用于仅限用于 R 脚本 （无 Python 等效项）。 适用于 （独立） 服务器选项，以避免与其他 SQL Server 操作的资源竞争。 |


## <a name="new-in-sql-server-2016"></a>SQL Server 2016 中的新增功能

此发行版引入了机器学习功能编程到 SQL Server 通过**SQL Server 2016 R Services**，对数据库引擎实例内的常驻数据处理 R 脚本的数据库中分析引擎。

此外， **SQL Server 2016 R Server （独立）**发布为一种方法在 Windows server 上安装 R Server。 最初，SQL Server 安装程序提供安装 R Server for Windows 的唯一方法。 在更高版本中，开发人员和数据科学家他们希望在 Windows 上的 R Server 可以使用另一个独立安装程序来完成相同的目标。 SQL Server 中的独立服务器在功能上等效于独立服务器产品， [Microsoft R Server for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

| 发行版本 |功能更新 |
|---------|----------------|
| CU | [**实时评分**](real-time-scoring.md)依赖于本机 c + + 库读取优化的二进制格式，存储在模型，然后无需调用 R 运行时生成预测。 这使得评分操作快得多。 与实时评分，可以运行存储的过程或执行实时评分 R 代码中。 也可用于 SQL Server 2016 中，如果实例升级到最新版本的实时评分是[!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]。 |
| 初始版本 | [**数据库中分析的 R 集成**](r/sql-server-r-services.md)。 <br/><br/> 调用 R 的 R 包函数 T-SQL，反之亦然。 RevoScaleR 函数通过分为组件的字符串，协调分块数据提供大规模的 R 分析和管理分布式处理和聚合结果。 在 SQL Server 2016 R Services （数据库），RevoScaleR 引擎与数据库引擎实例，或数据和分析一起相同处理上下文中相集成。 <br/><br/>通过的 T-SQL 和 R 集成[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 你可以调用任何使用此存储的过程的 R 代码。 此安全基础结构使 Rn 模型和脚本，可以从使用简单的存储的过程的应用程序调用的企业级部署。 可通过从 SQL 与 R 进程 MPI 环并行化的流式处理数据来实现更多的性能提升。 <br/><br/>你可以使用 T-SQL 的[预测](../t-sql/queries/predict-transact-sql.md)函数来执行[本机评分](sql-native-scoring.md)上预先训练的模型已以前保存在所需的二进制格式。|

## <a name="linux-support-roadmap"></a>Linux 支持路线图

在 Linux 上的 SQL Server 中，当前不支持使用 R 或 Python 数据库中的机器学习。 查看我们的更高版本中的通知。

但是，在 Linux 上可以执行[本机评分](sql-native-scoring.md)使用 T-SQL 的预测函数。 本机评分，可以从预先训练的模型非常快，评分而无需调用或甚至需要的 R 运行时。 这意味着可以在 Linux 上使用 SQL Server 来生成预测非常快，以便为客户端应用程序提供服务。

## <a name="next-steps"></a>后续步骤

+ [安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](install/sql-machine-learning-services-windows-install.md)
+ [机器学习教程和示例](tutorials/machine-learning-services-tutorials.md)
