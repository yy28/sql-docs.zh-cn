---
title: SQL Server 机器学习服务器 （独立版） 和 R Server （独立版） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8cdceabc26c55b6eade57712fa610d3e84808f5
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174784"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server 机器学习服务器 （独立版） 和 R Server （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

独立服务器是机器学习组件，表达为 R 和 Python 的功能，运行独立于 SQL Server 数据库引擎实例的安装。 SQL Server 上没有依赖项，可以其本身而言，安装在独立服务器。 由于独立的服务器是独立于 SQL Server、 配置和管理任务和工具均更类似于非 SQL 版本的机器学习服务器，您可以在中阅读有关[这篇文章](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。

独立机器学习服务器的目的是提供丰富的开发环境，与对小型到大型数据集，使用的专有包和计算引擎的 R 和 Python 工作负荷的分布式和并行处理与服务器一起安装。 独立服务器上的 R 和 Python 包为不同于在 SQL Server （数据库） 安装中，从而使代码可移植性提供并[计算上下文切换](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

主要原因开发人员选择独立机器学习服务器是超越的开源 R 和 Python 的内存和处理约束。 独立服务器可以加载和处理大量数据的多个核心上并聚合到单个合并输出结果。 函数和算法设计规模和实用程序： 提供预测分析、 统计建模、 数据可视化效果和先进的机器学习算法中的商业服务器产品设计和支持Microsoft。

通常情况下，我们建议您将 （独立版） 并 （数据库内） 安装为相互独占以避免资源争用，但如果您有足够的资源，没有针对在同一台物理计算机上安装这两个不禁止。

只能在计算机上有一台独立服务器： 任一[SQL Server 2017 机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)或[SQL Server 2016 R Server （独立版）](../install/sql-r-standalone-windows-install.md)。 您必须手动卸载然后再安装不同版本的一个版本。

## <a name="components-of-a-standalone-server"></a>独立服务器的组件

SQL Server 2016 仅为 R。 SQL Server 2017 支持 R 和 Python。 下表介绍每个版本中的功能。

| 组件 | Description |
|-----------|-------------|
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

+ [SQL Server 2017 机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （独立版）-仅 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步骤 2： 配置开发工具

配置您的开发工具使用 Machine Learning Server 二进制文件。 有关 Python 的详细信息，请参阅[链接 Python 二进制文件](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 有关如何在 R Studio 中连接的说明，请参阅[使用不同的版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) ，该工具指向 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64。 此外可以尝试[针对 Visual Studio 的 R 工具](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

### <a name="step-3-write-your-first-script"></a>第 3 步： 编写第一个脚本

编写使用 RevoScaleR 和 revoscalepy，机器学习算法中的函数的 R 或 Python 脚本。
  
  + [探索 R 和 25 个函数的 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 开始使用 R 的基本命令，然后提供高性能的 RevoScaleR 可分发分析函数的进度和缩放 R 解决方案。 包括许多最流行的 R 建模包的可并行化版本，例如 K-均值聚类、决策树和决策林以及用于数据操作的工具。

  + [快速入门： 使用 microsoftml Python 包的二进制分类的示例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)： 创建使用从 microsoftml 和已知乳腺癌癌症数据集的函数的二元分类模型。

选择该任务的最佳语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的操作数据，充分利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为了实现最佳性能。 对列进行快速计算时，可使用内存数据库引擎。

### <a name="step-4-operationalize-your-solution"></a>步骤 4： 操作你的解决方案

可以使用独立的服务器[实施](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL 品牌[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 可以配置独立的服务器的操作化，可以为您提供这些优点： 部署和托管你的代码，因为 web 服务，运行诊断程序，测试 web 服务容量。

## <a name="see-also"></a>另请参阅

 [SQL Server 机器学习服务 （数据库内）](sql-server-r-services.md)

