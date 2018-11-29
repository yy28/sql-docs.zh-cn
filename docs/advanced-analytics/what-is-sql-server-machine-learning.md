---
title: R 和 Python 机器学习 SQL Server 中的服务 |Microsoft Docs
description: 在 SQL Server 和 Python 在 SQL Server 中，与用于数据科学和统计建模、 机器学习模型，预测分析、 数据可视化效果和的详细信息的关系数据集成的 R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0768ae40b110bbb2b85890f0a8b4eff0339cedde
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269700"
---
# <a name="machine-learning-services-r-python-in-sql-server-2017"></a>SQL Server 2017 中机器学习服务 （R、 Python）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017机器学习服务是数据库引擎实例的加载项，用于在 SQL Server 上执行 R 和 Python 代码。 代码在可扩展性框架中运行，与核心引擎进程隔离，但完全可用于关系数据（作为存储过程、包含 R 或 Python 语句的 T-SQL 脚本或包含 T-SQL 的 R 或 Python 代码）。 

如果以前使用过[SQL Server 2016 R Services](r/sql-server-r-services.md)、 SQL Server 2017 中的机器学习服务是与更新版本的基本 R，RevoScaleR，MicrosoftML，R 支持，下一代和 2016 版本中引入的其他库。 

在 Azure SQL 数据库中，[机器学习服务（使用 R)]((https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-r))目前处于公共预览状态。

机器学习服务的关键价值主张是其企业R和Python软件包的强大功能，可以大规模提供高级分析，并能够将计算和处理带到数据所在的位置，从而消除了在网络上提取数据的需求。

## <a name="components"></a>组件

SQL Server 2017 支持 R 和 Python。 下表描述了这些组件。

| 组件 | Description |
|-----------|-------------|
| SQL Server Launchpad服务 | 管理外部R和Python运行时与数据库引擎实例之间通信的服务。 |
| R 包 | [**RevoScaleR** ](r/revoscaler-overview.md)是主库的此库中的可缩放。 函数是最广泛使用。 这些库中找到数据转换和操作、 统计汇总、 可视化和建模和分析多种形式。 此外，这些库中的函数会自动将工作负荷分散到以便并行处理，能够工作的协调和管理计算引擎的数据块上的可用内核。  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义文本分析、 图像分析和情绪分析模型。 <br/>[**sqlRUtils** ](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)用于 R 脚本置于 T-SQL 存储过程、 向数据库注册存储的过程和从 R 开发环境运行存储的过程提供帮助器函数。<br/>[**olapR** ](r/how-to-create-mdx-queries-using-olapr.md)是用于构建还是在 R 脚本中执行 MDX 查询。|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open)是 Microsoft 的开放源代码分发的。包含包和解释器。 始终使用 MRO 由安装程序安装的版本。 |
| R 工具 | R 控制台窗口和命令提示是 R 分发版中的标准工具。  |
| R 示例和脚本 |  开源 R 和 RevoScaleR 包中包含内置数据集，以便你可以使用预安装的数据创建和运行脚本。 |
| Python 包 | [**revoscalepy** ](python/what-is-revoscalepy.md) 是可缩放 Python 的主要库，具有用于数据操作、转换、可视化和分析的函数。 <br/>[**microsoftml (Python)** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 添加了机器学习算法，用于为文本分析、图像分析和情绪分析创建自定义模型。  |
| Python 工具 | 内置的 Python 命令行工具，可用于临时测试和多种任务。  |
| Anaconda | Anaconda 是 Python 的开源分发版，包含大量基本包。 |
| Python 示例和脚本 | 与  R一样，Python 包含内置的数据集和脚本。  |
| R 和 Python 中预先训练的模型 | 预先训练的模型为特定用例而创建，由 Microsoft 的数据科学工程团队维护。 可以按原样使用预先训练的模型对文本中的积极/消极情绪进行评分，或者使用你提供的新数据输入检测图像中的特征。 这些模型在机器学习服务中运行，但不能通过 SQL Server 安装程序安装。 有关详细信息，请参阅[在 SQL Server 上安装预先训练的机器学习模型](install/sql-pretrained-models-install.md)。 |

## <a name="using-sql-mls"></a>使用 SQL MLS

开发人员和分析人员通常在本地SQL服务器实例上运行代码。 通过添加机器学习服务并启用外部脚本执行，您可以在SQL Server模式中运行R和Python代码:将脚本包装在存储过程中，将模型存储在SQL Server表中，或者在查询中组合T-SQL和R或Python函数。

脚本执行位于数据安全模型的边界内：关系数据库的权限是脚本中数据访问的基础。 运行R或Python脚本的用户不应该能够使用SQL查询中该用户无法访问的任何数据。 您需要标准数据库读取和写入权限，以及运行外部脚本的其他权限。 为关系数据编写的模型和代码包装在存储过程中，或者序列化为二进制格式并存储在表中，或者如果将原始字节流序列化为文件，则从磁盘加载。

数据库内分析最常用的方法是使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，将R或Python脚本作为输入参数传递。

经典的客户端-服务器交互是另一种方法。 从任何客户端工作站上具有一个 IDE，可以安装[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)或[Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)，然后编写将推送执行的代码 (称为*远程计算上下文*) 对数据和到远程 SQL Server 的操作。 

最后，如果使用的[独立服务器](r/r-server-standalone.md)和 Developer edition 中，你可以构建解决方案，客户端工作站上使用相同的库和解释器，并随后部署生产代码中的对 SQL Server 机器学习服务 （数据库内）。 

## <a name="how-to-get-started"></a>如何开始

### <a name="step-1-install-the-software"></a>步骤 1： 安装软件

+ [SQL Server 机器学习服务 （数据库内）](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步骤 2： 配置开发工具

数据科研人员通常在自己的笔记本电脑或开发工作站上使用 R 或 Python 来研究数据并生成和调整预测模型，直到生成效果良好的预测模型。 使用 SQL Server 中的数据库内分析，没有必要更改此过程。 安装完成后，您可以在 SQL Server 上运行 R 或 Python 代码，本地和远程。

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **使用喜欢的 IDE**。 你可以链接到所选的开发工具的 R 和 Python 库。 有关详细信息，请参阅[设置的 R 工具](r/set-up-a-data-science-client.md)并[设置 Python 工具](python/setup-python-client-tools-sql.md)。  

+ **处理远程或本地**。 数据科研人员可以像平时一样连接到 SQL Server，然后将数据取回到客户端进行本地分析。 但是，更好的解决方案是使用**RevoScaleR**或**revoscalepy** Api 将计算推送到 SQL Server 计算机，避免成本高昂且不安全的数据移动。

+ **在 SQL Server 存储过程中嵌入 R 或 Python 脚本**。 代码充分优化后，将其封装在一个存储过程中，以避免不必要的数据移动和优化数据处理任务。

### <a name="step-3-write-your-first-script"></a>第 3 步： 编写第一个脚本

调用 R 或 Python 中的函数从 T-SQL 脚本：

+ [： 了解使用 R 的数据库内分析](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [： 使用 R 的端到端演练](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python：使用 T-SQL 运行 Python](tutorials/run-python-using-t-sql.md)
+ [Python： 了解数据库内分析使用 Python](tutorials/sqldev-in-database-python-for-sql-developers.md)

选择该任务的最佳语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的操作数据，利用 SQL Server 的强大功能实现最佳性能。 对列进行快速计算时，可使用内存数据库引擎。

### <a name="step-4-optimize-your-solution"></a>步骤 4： 优化你的解决方案

当模型可基于企业数据进行扩展时，数据科学家往往会与 DBA 或 SQL 开发人员合作以优化以下流程：

+ 特征工程
+ 数据引入和数据转换
+ 评分

传统上，使用 R 的数据科学家会遇到性能和规模方面的问题，使用大型数据集时尤其如此。这是因为公共运行时实现是单线程的，并且只能容纳适合本地计算机上可用内存的那些数据集。与 SQL Server 机器学习服务集成可提供多种功能，有助于提升性能，同时还可提供更多数据：

+ **RevoScaleR**： 此 R 包包含一些最常用的 R 函数，经过重新设计可提供并行性和扩展性。此包还包括一些功能，可通过将计算推送到 SQL Server 计算机来进一步提高性能和扩展性，这些计算机通常具有更大内存和更强的计算能力。

+ **revoscalepy**。该 Python 库实现了 RevoScaleR 中最常用的函数（例如远程计算上下文）以及许多支持分布式处理的算法。
 
有关性能的详细信息，请参阅此[性能案例研究](r/performance-case-study-r-services.md)并[R 和数据优化](r/r-and-data-optimization-r-services.md)。

### <a name="step-5-deploy-and-consume"></a>步骤 5： 部署和使用

准备好进行生产环境中使用的脚本或模型后，数据库开发人员可能会嵌入代码或模型中的存储过程，以便可以从应用程序调用的已保存的 R 或 Python 代码。 存储和从 SQL Server 中运行 R 代码可带来诸多好处： 可以使用方便的 SQL Server 界面中，且所有计算都发生在数据库中，从而避免不必要的数据移动。

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **安全且可扩展**。 SQL Server 使用新的可扩展性体系结构，可在数据库引擎的安全并隔离 R 和 Python 的会话。 你还可以控制用户可以执行脚本，并可以指定的代码可以访问哪些数据库。 您可以控制分配给运行时，以防止海量计算降低服务器的整体性能的资源量。

+ **计划和审核**。 在 SQL Server 中运行外部脚本作业时，可以控制和审核数据研究人员使用的数据。 与计划其他任何 T-SQL 作业和存储过程一样，用户还可以计划作业和创作包含外部 R 或 Python 脚本的工作流。

若要充分利用资源管理和安全功能的 SQL Server 中，部署过程可能会包括这些任务：

+ 将你的代码转换为可以在存储过程中以最佳方式运行的函数
+ 设置安全性并锁定使用某个特定任务的包
+ （需要企业版） 启用资源调控

有关详细信息，请参阅[R 的资源调控](r/resource-governance-for-r-services.md)并[SQL Server 的 R 包管理](r/install-additional-r-packages-on-sql-server.md)。

## <a name="version-history"></a>版本历史记录

SQL Server 2017 机器学习服务是新一代的 SQL Server 2016 R Services，增强，其中包括 Python。 下表是所有产品版本中，从开始到当前版本的完整列表。 

| 产品名称 | 引擎版本 | 发布日期 |
|--------------|---------|--------------|
| SQL Server 2017 机器学习服务 （数据库内） | R Server 9.2.1 <br/> Python 服务器 9.2 | 2017 年 10 月 |
| SQL Server 2017 机器学习服务器 （独立版） | R Server 9.2.1 <br/> Python 服务器 9.2 | 2017 年 10 月 |
| SQL Server 2016 R Services （数据库内） | R Server 9.1  | 2017 年 7 月  |
| SQL Server 2016 R Server （独立版）  |  R Server 9.1 | 2017 年 7 月 |

有关版本的包版本，请参阅中的映射的版本[升级 R 和 Python 组件](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map)。

## <a name="portability-and-related-products"></a>可移植性和相关产品

包含我们的 R 和 Python 解释器的免费客户端包括 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 和 [Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

包含我们的R和Python解释器的免费客户端是[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)并[Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)。

在 Azure 中，Microsoft 的 R 和 Python 包和解释器也在 Azure 机器学习、Azure 服务（如 [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight)）以及 [Azure 虚拟机](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux) 中提供。Data Science Virtual Machine(https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) 具有一个配备齐全的开发工作站，其中包含多家供应商提供的工具以及 Microsoft 的库和解释器。

## <a name="see-also"></a>请参阅

[安装 SQL Server 机器学习服务](install/sql-machine-learning-services-windows-install.md)
