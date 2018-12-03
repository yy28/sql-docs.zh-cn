---
title: SQL Server 中的独立的 R Server 或 Machine Learning Server 安装 |Microsoft Docs
description: 为独立版 R Server 概述简介和机器学习服务器在 SQL Server 安装程序
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9cb0cecaef28d512cf36e694344e62b01df88ebf
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657496"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server （独立版） 和 SQL Server 中的机器学习服务器 （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 提供独立的 R Server 或运行独立于 SQL Server 的机器学习服务器安装支持。 具体取决于 SQL Server 版本，独立的服务器具有的开放源代码 R 和可能是 Python，叠加的大规模添加统计和预测分析的高性能库从 Microsoft 的基础。 库还使在 R 或 Python 中编写脚本的机器学习任务。 

在 SQL Server 2016 中，此功能称为**R Server （独立版）** 是仅限 R 的。 在 SQL Server 2017 中，名为**Machine Learning Server （独立版）** 并包括 R 和 Python。  

> [!Note]
> 独立服务器由 SQL Server 安装程序安装，在功能上等同于 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) 的非 SQL 品牌版本，支持相同的用户场景，包括远程执行、操作和 Web 服务，以及 R 和 Python 的完整集合库。

## <a name="components"></a>组件

SQL Server 2016 仅为 R。 SQL Server 2017 支持 R 和 Python。 下表介绍每个版本中的功能。

| 组件 | Description |
|-----------|-------------|
| R 包 | [**RevoScaleR** ](revoscaler-overview.md) 是可扩展 R 的主要库，包含数据操作、转换、可视化和分析功能。  <br/>[**MicrosoftML** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 可添加机器学习算法，以创建用于文本分析、图像分析和情感分析的自定义模型。 <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) 可提供帮助程序函数，从而将 R 脚本放入 T-SQL 存储过程，向数据库注册存储过程，以及从 R 开发环境运行存储过程。<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) 可提供 Web 服务部署（仅在 SQL Server 2017 中）。 <br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md) 可用于在 R 中指定 MDX 查询。|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) 是 Microsoft 提供的 R 的开源分发版，内含包和解释器。始终使用安装程序中附带的 MRO 版本。 |
| R 工具 | R 控制台窗口和命令提示符是 R 分发版中的标准工具。可在 \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 中找到它们。 |
| R 示例和脚本 | 开源 R 和 RevoScaleR 包中包含内置数据集，你可以使用预安装的数据创建和运行脚本。可在 Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR 中找到它们。 |
| Python 包 | [**revoscalepy** ](../python/what-is-revoscalepy.md) 是可缩放 Python 的主要库，具有数据操作、转换、可视化和分析功能。<br/>[**microsoftml** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 添加了机器学习算法，以创建用于文本分析、图像分析和情绪分析的自定义模型。 |
| Python 工具 | 内置的 Python 命令行工具可用于临时测试和任务。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 中找到该工具。 |
| Anaconda | Anaconda 是 Python 和必备包的开源分发版。 |
| Python 示例和脚本 | 与 R 一样，Python 包含内置数据集和脚本。请在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data 中查找 revoscalepy 数据。|
| R 和 Python 中预先训练的模型 | 针对特定用例创建预先训练的模型，并由Microsoft的数据科学工程团队维护。您可以使用预先训练的模型按原样评估文本中的正负情绪，或使用您提供的新数据输入检测图像中的特征。预先训练的模型在独立服务器上受支持和可用，但您无法通过SQL Server安装程序进行安装。有关更多信息，请参阅[在SQL Server上安装预训练机器学习模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-a-standalone-server"></a>使用独立服务器

R 和 Python 开发人员通常选择要移动的开源 R 和 Python 的内存和处理约束超过的独立服务器。 在独立服务器上执行的 R 和 Python 库可以加载和处理大量数据的多个核心上并聚合到单个合并输出结果。 规模和实用程序设计为高性能函数： 交付预测分析、 统计建模、 数据可视化功能以及先进的机器学习算法中的商业服务器产品设计和支持Microsoft。

从 SQL Server 中分离的独立服务器，作为 R 和 Python 环境配置，保护安全和访问使用基础操作系统和独立服务器，非 SQL Server 中提供的标准工具。 没有 SQL Server 关系数据的内置支持。 如果你想要使用 SQL Server 数据，您可以创建数据源对象和连接，就像从任何客户端。

为 SQL Server 的附加补充，独立服务器如果则也可以作为功能强大的开发环境需要本地和远程计算。 在独立服务器上的 R 和 Python 包为与提供的数据库引擎安装，从而使代码可移植性相同和[计算上下文切换](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

## <a name="how-to-get-started"></a>如何开始

开始安装程序，将二进制文件附加到您最喜欢的开发工具，编写第一个脚本。

### <a name="step-1-install-the-software"></a>步骤 1： 安装软件

安装以下任一版本：

+ [SQL Server 2017 机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （独立版）-仅 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步骤 2： 配置开发工具

在独立服务器上，通常使用安装在同一台计算机上的开发工具在本地工作。

+ [设置 R 工具](set-up-a-data-science-client.md)
+ [设置 Python 工具](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>第 3 步： 编写第一个脚本

使用RevoScaleR，revoscalepy和机器学习算法中的函数编写R或Python脚本。
  
  + [探索R和RevoScaleR中的25个功能](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)：从基本的R命令开始，然后进入RevoScaleR可分配的分析功能，为R解决方案提供高性能和扩展。包括许多最流行的R建模软件包的可并行化版本，例如k-means集群，决策树和决策林，以及用于数据操作的工具。

  + [快速入门： 使用 microsoftml Python 包的二进制分类的示例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)： 使用microsoftml和众所周知的乳腺癌数据集中的函数创建二进制分类模型。


选择最适合该任务的语言。 R最适合于使用SQL难以实现的统计计算。对于基于集合的数据操作，利用SQL Server的强大功能来实现最高性能。使用内存数据库引擎可以非常快速地对列进行计算。

### <a name="step-4-operationalize-your-solution"></a>步骤 4： 操作你的解决方案


独立服务器可以使用非SQL品牌的[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)的操作功能(https://docs.microsoft.com//machine-learning-server/what-is-operationalization)。您可以配置独立服务器进行操作，从而为您带来以下好处：将代码部署和托管为Web服务，运行诊断程序，测试Web服务容量。

## <a name="see-also"></a>请参阅

 [安装 R Server （独立版） 或机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)

