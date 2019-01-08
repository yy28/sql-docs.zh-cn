---
title: 独立的 R Server 或机器学习服务器安装的 SQL Server 机器学习服务
description: 为独立版 R Server 概述简介和机器学习服务器在 SQL Server 安装程序
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f1cbc4a7c02597c6c8bece8c47976fabdb4959e7
ms.sourcegitcommit: 0bb306da5374d726b1e681cd4b5459cb50d4a87a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2018
ms.locfileid: "53731974"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server （独立版） 和 SQL Server 中的机器学习服务器 （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 为独立于 SQL Server 运行的独立 R Server 或 Machine Learning Server 提供安装支持。 根据 SQL Server 版本，独立服务器具有开放源 R 和 Python（可能具有）的基础，再加上可大规模添加统计和预测分析的 Microsoft 高性能库。 这些库还支持用 R 或 Python 编写脚本的机器学习任务。 

在 SQL Server 2016 中，此功能称为**R Server （独立版）** 是仅限 R 的。 在 SQL Server 2017 中，名为**Machine Learning Server （独立版）** 并包括 R 和 Python。  

> [!Note]
> 独立服务器由 SQL Server 安装程序安装，在功能上等同于 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) 的非 SQL 品牌版本，支持相同的用户场景，包括远程执行、操作和 Web 服务，以及 R 和 Python 的完整集合库。

## <a name="components"></a>组件

SQL Server 2016 仅适用于 R。 SQL Server 2017 支持 R 和 Python。 下表介绍每个版本中的功能。

| 组件 | Description |
|-----------|-------------|
| R 包 | [**RevoScaleR** ](ref-r-revoscaler.md) 是可扩展 R 的主要库，包含数据操作、转换、可视化和分析功能。  <br/>[**MicrosoftML** ](ref-r-microsoftml.md) 可添加机器学习算法，以创建用于文本分析、图像分析和情感分析的自定义模型。 <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) 可提供帮助程序函数，从而将 R 脚本放入 T-SQL 存储过程，向数据库注册存储过程，以及从 R 开发环境运行存储过程。<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) 可提供 Web 服务部署（仅在 SQL Server 2017 中）。 <br/>[**olapR** ](ref-r-olapr.md) 可用于在 R 中指定 MDX 查询。|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) 是 Microsoft 提供的 R 的开源分发版，内含包和解释器。 始终使用安装程序中附带的 MRO 版本。 |
| R 工具 | R 控制台窗口和命令提示符是 R 分发版中的标准工具。 可在  \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64 中找到它们。 |
| R 示例和脚本 |  开源 R 和 RevoScaleR 包中包含内置数据集，你可以使用预安装的数据创建和运行脚本。 可在 Program files\Microsoft SQL Server\140\R_SERVER\library\datasets 和 \library\RevoScaleR 中找到它们。 |
| Python 包 | [**revoscalepy** ](../python/ref-py-revoscalepy.md) 是可缩放 Python 的主要库，具有数据操作、转换、可视化和分析功能。 <br/>[**microsoftml** ](../python/ref-py-microsoftml.md) 添加了机器学习算法，以创建用于文本分析、图像分析和情绪分析的自定义模型。  |
| Python 工具 | 内置的 Python 命令行工具可用于临时测试和任务。 在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe 中找到该工具。 |
| Anaconda | Anaconda 是 Python 和必备包的开源分发版。 |
| Python 示例和脚本 | 与 R 一样，Python 包含内置数据集和脚本。 请在 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data 中查找 revoscalepy 数据。 |
| R 和 Python 中预先训练的模型 | 预先训练的模型针对特定用例创建，并由 Microsoft 的数据科学工程团队维护。 可以按原样使用预先训练的模型对文本中的积极/消极情绪进行评分，或使用你提供的新数据输入检测图像中的特征。 预先训练的模型在独立服务器上受支持并且可用，但不能通过 SQL Server 安装程序进行安装。 有关详细信息，请参阅[在 SQL Server 上安装预训练的机器学习模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-a-standalone-server"></a>使用独立服务器

R 和 Python 开发人员通常选择要移动的开源 R 和 Python 的内存和处理约束超过的独立服务器。 在独立服务器上执行的 R 和 Python 库可以加载和处理大量数据的多个核心上并聚合到单个合并输出结果。 规模和实用程序设计为高性能函数： 交付预测分析、 统计建模、 数据可视化功能以及先进的机器学习算法中的商业服务器产品设计和支持Microsoft。

从 SQL Server 中分离的独立服务器，作为 R 和 Python 环境配置，保护安全和访问使用基础操作系统和独立服务器，非 SQL Server 中提供的标准工具。 没有 SQL Server 关系数据的内置支持。 如果你想要使用 SQL Server 数据，您可以创建数据源对象和连接，就像从任何客户端。

为 SQL Server 的附加补充，独立服务器如果则也可以作为功能强大的开发环境需要本地和远程计算。 在独立服务器上的 R 和 Python 包为与提供的数据库引擎安装，从而使代码可移植性相同和[计算上下文切换](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。

## <a name="how-to-get-started"></a>如何开始

从安装开始，将二进制文件附加到您最喜欢的开发工具上，并编写第一个脚本。

### <a name="step-1-install-the-software"></a>步骤 1：安装软件

安装这些版本的之一：

+ [SQL Server 2017 机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server （独立版）-仅 R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>步骤 2：配置开发工具

在独立服务器上，很常见，若要运行使用本地安装在同一台计算机上的开发。

+ [设置 R 工具](set-up-a-data-science-client.md)
+ [设置 Python 工具](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>步骤 3：编写第一个脚本

编写使用 RevoScaleR 和 revoscalepy，机器学习算法中的函数的 R 或 Python 脚本。
  
  + [探索 R 和 25 个函数的 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler):开始基本 R 命令，然后转到提供高性能和缩放 R 解决方案的 RevoScaleR 可分发分析函数。 包括许多最流行的 R 建模包的可并行化版本，例如 K-均值聚类、决策树和决策林以及用于数据操作的工具。

  + [快速入门：Microsoftml Python 包与二进制分类的示例](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml):创建使用从 microsoftml 和已知乳腺癌癌症数据集的函数的二元分类模型。

选择最适合任务的语言。 使用 SQL 难以实现统计计算，但适合使用 R 来实现。 对于基于集的操作数据，充分利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为了实现最佳性能。 对列进行快速计算时，可使用内存数据库引擎。

### <a name="step-4-operationalize-your-solution"></a>步骤 4：实施你的解决方案

可以使用独立的服务器[实施](https://docs.microsoft.com//machine-learning-server/what-is-operationalization)功能的非 SQL 品牌[Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)。 可以配置独立的服务器的操作化，可以为您提供这些优点： 部署和托管你的代码，因为 web 服务，运行诊断程序，测试 web 服务容量。

### <a name="step-5-maintain-your-server"></a>步骤 5：维护你的服务器

SQL Server 版本定期的累积更新。 应用累积更新将安全性和功能的增强功能添加到现有安装。 

新的或已更改功能的说明可在[CAB 下载](../install/sql-ml-cab-downloads.md)一文和 web 页上[SQL Server 2016 累积更新](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)和[SQL Server 2017 累积更新](https://support.microsoft.com/help/4047329). 

有关如何将更新应用于现有实例的详细信息，请参阅[应用更新](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)安装说明中。

## <a name="see-also"></a>另请参阅

 [安装 R Server （独立版） 或机器学习服务器 （独立版）](../install/sql-machine-learning-standalone-windows-install.md)

