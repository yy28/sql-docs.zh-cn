---
title: SQL Server 计算机学习服务器 （独立） 和 R Server （独立） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2c416049692f8860e4ba608e58f401ce527b135c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203039"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server 计算机学习服务器 （独立） 和 R Server （独立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

独立服务器是机器学习组件，说明哪些情况下作为 R 和 Python 的功能，可运行独立于 SQL Server 数据库引擎实例的安装。 你可以安装独立服务器本身，SQL Server 上没有依赖项。 因为独立服务器是独立于 SQL Server、 配置和管理任务和工具均更类似于机器学习服务器，你可以阅读中的非 SQL 版本[本文](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。

Server 的独立机学习的目的是提供丰富的开发环境中，分布式和并行处理对小型到大型数据集，使用专有的包和计算引擎的 R 和 Python 工作负荷与服务器一起安装。 在独立服务器上的 R 和 Python 包是不同于提供在 SQL Server （数据库中） 安装中，从而使代码可移植性和[计算上下文切换](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

主要原因开发人员选择独立机器学习服务器是超越开放源代码 R 和 Python 的内存和处理约束。 独立服务器可以加载和处理大量的数据上的多个核心以及聚合到单个合并输出结果。 函数和算法的设计以实现缩放和实用程序： 提供预测分析、 统计建模、 数据可视化效果和先进的机器学习算法在商业服务器产品中的设计和支持Microsoft。

通常情况下，我们建议您将 （独立版），并且 （数据库中） 安装为相互排斥若要避免资源争用，但如果你有足够的资源，没有针对在同一台物理计算机上安装这两个不禁止。

在计算机上只能有一台独立服务器： 任一[SQL Server 自 2017 年 1 机器学习服务器 （独立）](../install/sql-machine-learning-standalone-windows-install.md)或[SQL Server 2016 R Server （独立）](../install/sql-r-standalone-windows-install.md)。 你必须手动卸载然后再安装不同版本的一个版本。

## <a name="components-of-a-standalone-server"></a>独立服务器的组件

SQL Server 2016 仅 R。 SQL Server 2017 支持 R 和 Python。 下表介绍每个版本中的功能。

| 组件 | Description |
|-----------|-------------|
| R 包 | [RevoScaleR](revoscaler-overview.md)主库用于可扩展 R 具有可实现数据操作、 转换、 visualzation 和分析功能。  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义模型进行文本分析、 图像分析和观点分析。 <br/>[mrsdeploy](operationalization-with-mrsdeploy.md)提供 web 服务部署 （在 SQL Server 自 2017 年 1 仅)。 <br/>[olapR](how-to-create-mdx-queries-using-olapr.md)可用于指定 MDX 查询中。|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open)是 Microsoft 的开放源代码分发的。将包含包和解释器。 始终使用 MRO 捆绑到安装程序中的版本。 |
| R 工具 | R 控制台窗口和命令提示是 R 分发中的标准工具。 在 files\microsoft SQL Server\140\R_SERVER\bin\x64 中找到它们。 |
| R 示例和脚本 |  开放源代码 R 和 RevoScaleR 包中包含内置的数据集，以便你可以创建和运行脚本使用预安装的数据。 查看为其 files\microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR。 |
| Python 包 | [revoscalepy](../python/what-is-revoscalepy.md)主库用于可扩展 Python 具有可实现数据操作、 转换、 visualzation 和分析功能。 <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义模型进行文本分析、 图像分析和观点分析。  |
| Python 工具 | 内置的 Python 命令行工具可用于临时测试和任务。 在 files\microsoft SQL Server\140\PYTHON_SERVER\python.exe 找到该工具。 |
| Anaconda | Anaconda 是 Python 和基本包的一个开源分发。 |
| Python 示例和脚本 | 与 R，Python 包括内置的数据集和脚本。 在 files\microsoft SQL 查找 revoscalepy 数据 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 数据。 |
| 预先训练的模型中 R 和 Python | 预先训练的模型是受支持且可用在独立服务器上，但无法通过 SQL Server 安装程序安装。 Microsoft 机器学习 Server 的安装程序提供了模型，你可以安装免费。 有关详细信息，请参阅[安装预先训练的 SQL Server 上的机器学习模型](install-pretrained-models-sql-server.md)。 |

## <a name="get-started-step-by-step"></a>要开始分步

安装程序以开头、 将二进制文件附加到您喜爱的开发工具，和写入你的第一个脚本。

### <a name="step-1-install-the-software"></a>步骤 1： 安装软件

安装这些版本的之一：

+ [SQL Server 自 2017 年 1 机器学习服务器 （独立）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （独立）-仅 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步骤 2： 配置一个开发工具

配置你的开发工具，以使用机器学习服务器二进制文件。 有关 Python 的详细信息，请参阅[链接 Python 二进制文件](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 有关如何在 R Studio 中连接的说明，请参阅[使用不同的版本的 R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R)和指向 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 工具。 您还可以尝试[R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)。 

### <a name="step-3-write-your-first-script"></a>步骤 3： 编写第一个脚本

编写使用从 RevoScaleR、 revoscalepy 和机器学习算法的函数的 R 或 Python 脚本。
  
  + [浏览 R 和 25 函数中的 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)： 开始使用基本 R 命令，然后提供高性能的 RevoScaleR 可分发分析函数的进度和缩放到 R 解决方案。 包括许多最流行的 R 建模包的可并行化版本，例如 K-均值聚类、决策树和决策林以及用于数据操作的工具。

  + [快速入门： 使用 microsoftml Python 软件包的二元分类的示例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)： 创建使用从 microsoftml 和已知乳腺癌癌症数据集的函数的二元分类模型。

选择该任务的最佳语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的数据操作，利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以获得最大性能。 对列进行快速计算时，可使用内存数据库引擎。

### <a name="step-4-operationalize-your-solution"></a>步骤 4： 实施你的解决方案

可以使用独立服务器[操作化](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL 品牌[Microsoft 机器学习 Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 你可以配置操作化，这为你提供这些优势的独立服务器： 部署和托管你的代码，因为 web 服务，运行诊断程序，测试 web 服务容量。

## <a name="see-also"></a>另请参阅

 [SQL Server 机器学习服务 （数据库）](sql-server-r-services.md)

