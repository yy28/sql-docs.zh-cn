---
title: SQL Server 机器学习和 R Services （数据库） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 05a2a17988912d7066b0d9f6bf398b889a3cd882
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174774"
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server 机器学习和 R Services （数据库内）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

提供对 SQL Server 实例中驻留数据的 R 和 Python 外部脚本支持的 SQL Server 数据库引擎实例的上下文中运行的机器学习中数据库安装。 由于与集成机器学习[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以让分析贴近数据，并消除成本和与数据移动相关的安全风险。

由于数据库引擎是多实例，可以安装多个实例的数据库内分析，或甚至更低版本和较新版本的并排方案。 选项包括[SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-standalone-windows-install.md)使用 R 和 Python，或[SQL Server 2016 R Services （数据库内）](../install/sql-r-standalone-windows-install.md)只是 

机器学习组件还可安装为实例不可知[独立服务器](r-server-standalone.md)。 通常情况下，我们建议您将 （独立版） 并 （数据库内） 安装为相互独占以避免资源争用，如果您有足够的资源，但有针对这两个安装在同一台物理计算机上没有限制。

## <a name="choosing-between-in-database-and-standalone-analytics"></a>在数据库和独立分析之间进行选择

了解开发要求可以帮助您 （数据库） 之间进行选择和 （独立版） 方法。 独立服务器是更轻松地配置和管理如果希望最灵活的使用方式，或者如果你想要连接到不同的 SQL Server 外部的数据源。 

数据库内分析专为与 SQL Server 中的数据的深度集成。 可以编写调用 R 或 Python 函数，并在 SQL Server Management Studio 或任何工具或应用用于外部的或嵌入 T-SQL 中执行脚本的 T-SQL 查询。 如果你需要在中运行 R 或 Python 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，通过使用存储的过程或通过使用 SQL Server 实例作为[计算上下文](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)，必须安装在数据库内分析。 此选项提供最大数据安全并与 SQL Server 工具集成。

同时在数据库和独立服务器可以缓解这一开放源代码 R 和 Python 的内存和处理约束。 这两个选项包括相同的包和工具，能够加载和处理大量数据的多个核心上和聚合到单个合并输出结果。 函数和算法设计规模和实用程序： 提供预测分析、 统计建模、 数据可视化效果和先进的机器学习算法中的商业服务器产品设计和支持Microsoft。 

## <a name="components-of-an-in-database-installation"></a>在数据库中安装的组件

SQL Server 2016 仅为 R。 SQL Server 2017 支持 R 和 Python。 下表介绍每个版本中的功能。 除了 SQL Server Launchpad 服务，此表是等同于代码中提供[独立 server 文章](r-server-standalone.md)。

| 组件 | Description |
|-----------|-------------|
| SQL Server 快速启动板服务 | 用于管理外部的 R 和 Python 运行时之间的通信的服务和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 |
| R 包 | [RevoScaleR](revoscaler-overview.md)适用于具有可实现数据处理、 转换、 visualzation 和分析功能的可缩放 R 是主库。  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义文本分析、 图像分析和情绪分析模型。 <br/>[mrsdeploy](operationalization-with-mrsdeploy.md)产品/服务的 web 服务部署 （在仅 SQL Server 2017)。 <br/>[olapR](how-to-create-mdx-queries-using-olapr.md)用于在 R 中指定的 MDX 查询|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open)是 Microsoft 的开放源代码分发的。包含包和解释器。 始终使用 MRO 捆绑在一起安装程序中的版本。 |
| R 工具 | R 控制台窗口和命令提示中的 R 分发版的标准工具。 在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 中找到它们。 |
| R 示例和脚本 |  开放源代码 R 和 RevoScaleR 包包括内置的数据集，以便您可以创建和运行脚本使用预安装的数据。 为其查看 \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR。 |
| Python 包 | [revoscalepy](../python/what-is-revoscalepy.md)用于具有可实现数据处理、 转换、 visualzation 和分析功能可扩展 Python 是主库。 <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义文本分析、 图像分析和情绪分析模型。  |
| Python 工具 | 内置的 Python 命令行工具可用于临时测试和任务。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 中找到该工具。 |
| Anaconda | Anaconda 是开放源代码的 Python 和基本包的发行版本。 |
| Python 示例和脚本 | 如使用 R、 Python 包含内置的数据集和脚本。 在 \Program files\Microsoft SQL 查找 revoscalepy 数据 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 数据。 |
| R 和 Python 中预先训练的模型 | 预先训练的模型支持的和可用的独立服务器上，但您不能通过 SQL Server 安装程序安装它们。 Microsoft 机器学习服务器安装程序提供了模型，可以安装免费。 有关详细信息，请参阅[安装预先训练的机器学习模型，在 SQL Server 上](../install/sql-pretrained-models-install.md)。 |

## <a name="get-started-step-by-step"></a>入门分步

开始安装程序，将二进制文件附加到您最喜欢的开发工具，编写第一个脚本。

### <a name="step-1-install-the-software"></a>步骤 1： 安装软件

安装这些版本的之一：

+ [SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R Services （数据库内）-仅 R](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>步骤 2： 配置开发工具

配置您的开发工具使用 Machine Learning Server 二进制文件。 有关 Python 的详细信息，请参阅[链接 Python 二进制文件](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 有关如何在 R Studio 中连接的说明，请参阅[使用不同的版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) ，该工具指向 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64。 此外可以尝试[针对 Visual Studio 的 R 工具](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

数据科研人员通常在自己的笔记本电脑或开发工作站上使用 R 或 Python 来研究数据并生成和调整预测模型，直到生成效果良好的预测模型。 

使用 SQL Server 中的数据库内分析，没有必要更改此过程。 安装完成后，你可以在上运行 R 或 Python 代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本地或远程：

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **使用喜欢的 IDE**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 客户端组件为数据科研人员提供所有必要的工具来展开试验和开发。 这些工具包括 R 运行时、用于提升标准 R 操作性能的 Intel 数学内核库，以及一组支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中执行 R 代码的增强型 R 包。  

+ **处理远程或本地**。 数据科研人员可以像平时一样连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后将数据取回到客户端进行本地分析。 但是，更好的解决方案是使用**RevoScaleR**或**revoscalepy** Api 将计算推送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机，以避免成本高昂且不安全的数据移动。

+ **嵌入在 R 或 Python 脚本[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程**。 代码充分优化后，将其封装在一个存储过程中，以避免不必要的数据移动和优化数据处理任务。

### <a name="step-3-write-your-first-script"></a>第 3 步： 编写第一个脚本

调用 R 或 Python 中的函数从 T-SQL 脚本：
  
  + [R：在 Transact-SQL 中使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R：适用于 SQL 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python：使用 T-SQL 运行 Python](../tutorials/run-python-using-t-sql.md)
  + [Python：适用于 SQL 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

选择该任务的最佳语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的操作数据，充分利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为了实现最佳性能。 对列进行快速计算时，可使用内存数据库引擎。

### <a name="step-4-optimize-your-solution"></a>步骤 4： 优化你的解决方案

准备好根据企业数据缩放模型时，数据科研人员通常会与 DBA 或 SQL 开发人员一起优化以下流程非常有效：

+ 特征工程
+ 数据引入和数据转换
+ 计分

通常，使用 R 的数据科研人员在性能和伸缩性两方面都会遇到问题，尤其是在使用大型数据集时。 因为通用运行时实现是单线程的，只能适应可装入本地计算机上可用内存的数据集。 与 SQl Server 机器学习服务集成可以提供多种功能，带来更好的性能，并处理更多的数据：

+ **RevoScaleR**： 此 R 包包含部分最常用 R 函数，可提供并行度与伸缩性重新设计的实现实现。 该包还包含一些函数，可通过将计算数据推送到通常具有大得多的内存和计算能力的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机，来进一步提升性能和伸缩性。

+ **revoscalepy**。 此 Python 库，可在 SQL Server 2017 中，例如远程计算上下文中 RevoScaleR，实现最常用的函数和许多算法支持的分布式处理。

**资源**

+ [性能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 和数据优化](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>步骤 5： 部署和使用

脚本或模型供生产使用后，数据库开发人员可能会嵌入代码或模型中存储的过程，以便可以从应用程序调用保存的 R 或 Python 代码。 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储和运行 R 代码可带来诸多好处：可使用便利的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 接口，并且所有计算将在数据库中发生，从而避免不必要的数据移动。

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **安全且可扩展**。 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用新的可扩展性体系结构，可在数据库引擎的安全并隔离 R 和 Python 的会话。 你还可以控制用户可以执行脚本，并可以指定的代码可以访问哪些数据库。 您可以控制分配给运行时，以防止海量计算降低服务器的整体性能的资源量。

+ **计划和审核**。 外部脚本作业中的运行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以控制和审核数据由数据科学家。 与计划其他任何 T-SQL 作业和存储过程一样，用户还可以计划作业和创作包含外部 R 或 Python 脚本的工作流。

若要利用 SQL Server 中的资源管理和安全功能，建议在部署过程中执行以下任务：

+ 将 yourcode 转换为可以在存储过程中以最佳方式运行的函数
+ 设置安全性并锁定使用某个特定任务的包
+ （需要企业版） 启用资源调控

**资源**

+ [R 的资源调控](resource-governance-for-r-services.md)
+ [SQL Server 的 R 包管理](install-additional-r-packages-on-sql-server.md)

## <a name="see-also"></a>另请参阅

 [SQL Server 机器学习和 R Server （独立版）](sql-server-r-services.md)
