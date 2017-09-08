---
title: "什么 &#39; s 机器学习服务中的新增功能 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8719ec8be1c0f7b7b0dc72093707829c30ebbb3f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>什么是 SQL Server 中的机器学习服务中的新增功能

在 SQL Server 2016，Microsoft 引入了 SQL Server R Services，通过与 SQL Server 数据库引擎集成 R 语言支持企业级数据科学的功能。

SQL Server 2017 中添加了对常用 Python 语言的支持，机器学习变得更加强大。 对新语言的支持以及附带的新名称：**机器学习服务 （数据库）**。

捕获的最新的公告 ！ [在 SQL Server 2017 Python： 增强数据库中机器学习](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017-release-candidate-2"></a>什么是 SQL Server 自 2017 年 1 候选发布版 2 中的新增功能

Microsoft SQL Server 中的机器学习 Server 现在提供用于生成和部署计算机学习解决方案的全面支持。 下面是此版本的要点：

> [!IMPORTANT]
> 
> 在 Linux 上，或在 Azure SQL 数据库中运行 SQL Server 时，机器学习服务，包括使用 R 或 Python，当前不支持。 寻找更高版本中的更改。
> 
> 但是，使用预测函数的本机评分是目前支持的 Linux 版本。 
 
### <a name="in-database-python-integration"></a>数据库 Python 集成

可以在存储过程中运行 Python，也可以执行 Python 远程作为计算上下文中使用 SQL Server 计算机。 此集成将打开新的 Python 开发人员和数据科学家使用的 SQL Server 功能，例如从 Microsoft 浏览创新 vast 社区途径**revoscalepy**和**microsoftml**.

SQL Server 开发人员访问到广泛的 Python 库从开放源生态系统，包括如 scikit 常用框架的了解，Tensorflow、 Caffe 和 Theano/Keras。 

但运行的 Python 数据库中不只是为了机器学习;有大量的集成与 SQL，利用要提供更智能、 功能强大的解决方案的相应语言的优势的 Python 其他潜在应用程序。

+ **revoscalepy**

    此版本包括的最终版本**revoscalepy**，其中提供的可缩放的 Pythonic 等效流式处理中 RevoScaleR 的算法。 你可以创建用于线性和逻辑回归、 决策树，提升的树和随机林，所有可并行化，并且能够在远程计算上下文中运行的 Python 模型。

    有关详细信息，请参阅[什么是 revoscalepy](python/what-is-revoscalepy.md)。

+ Python 远程计算上下文

    此版本支持使用多个数据源和远程计算上下文。 在远程 SQL 服务器上，若要浏览数据或生成模型，而无需移动数据，数据科研人员或开发人员可以执行 Python 代码。 使用远程计算上下文要求**revoscalepy**。

+ 在 Microsoft 机器学习 Server （独立版） 中的 Python 支持

    SQL Server 2017 包括要安装 Python 和 R 平台的独立版本的选项。 通过使用机器学习服务器，您可以分发，而无需使用 SQL Server 扩展 R 或 Python 代码。

    有关在 Microsoft 机器学习 Server 中的 Python 使用的示例，请参阅[发布和使用的 Python 代码](python/publish-consume-python-code.md)。

### <a name="new-algorithms"></a>新的算法

**MicrosoftML** R 和 Python 的包将包含最先进的机器学习算法和数据转换可缩放或运行在远程计算上下文。 算法包括可自定义深层神经网络、 快速决策树和决策林、 线性回归和逻辑回归。

MicrosoftML 包附带 R 和 Python 接口，，和基于 Microsoft 机器学习 Server 版本 9.2.0。

有关详细信息，请参阅[简介 MicrosoftML](using-the-microsoftml-package.md)和[for Python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。

### <a name="operationalization"></a>操作化

此版本包含多个选项和功能来帮助你部署和分发机器学习任务：

+ 使用 T-SQL 的操作化

    使用 T-SQL 的 Python 的集成意味着你可以调用任何 Python 代码使用`sp_execute_external_script`。 此安全基础结构支持 Python 模型和脚本，可以从使用简单的存储的过程的应用程序调用的企业级部署。 其他性能是从 SQL Python 进程和 MPI 环并行化的流式处理数据。

+ **mrsdeploy** for Python

    **Mrsdeploy**包为 Microsoft R Server 现在支持部署的 Python 模型和脚本作为 web 服务，可用作机器学习 Server （独立） 中的一个选项。 它的工作原理的示例，请参阅[发布和使用的 Python 代码](python/publish-consume-python-code.md)。

+ 性能

    Microsoft 已推送的边界进行评分的性能。 与数据库中评分，我们处理每 100 万行倒数第二次使用 R 模型。 在此版本中，为新功能**实时评分**和**本机评分**支持单行评分和小型更好的性能以及批处理。 

### <a name="realtime-scoring-and-native-scoring"></a>实时评分和本机评分

实时评分依赖于本机 c + + 库读取优化的二进制格式，存储在模型，然后无需调用 R 运行时生成预测。 这使得评分操作快得多。

此外，此版本的 SQL Server 2017 包括本机的 T-SQL 函数以快速获得评分，可以在任何版本的 SQL Server，即使在 Linux 上运行。 该函数不需要安装的 R 或额外的配置。 这意味着你可以训练模型在其他位置，将其保存在 SQL Server，然后执行评分而不会调用。此功能被称为_本机评分_。

  - 本机评分是仅在 SQL Server 2017 中可用。 它使用 T-SQL 的函数，可以在任何版本的 SQL Server，包括 Linux 中运行。
 - 在 SQL Server 自 2017 年，和在 Microsoft 机器学习 Server 中，支持实时评分。 你可以 runa 存储过程或执行实时评分 R 代码中。
 - 实时评分也是可用于 SQL Server 2016 中，如果实例升级到最新版本的 Microsoft R Server。

有关详细信息，请参阅以下文章：

 + [实时评分](real-time-scoring.md)
 + [本机评分](sql-native-scoring.md)
 + [如何执行实时评分或本机评分](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-ml-experience-and-get-pre-trained-models"></a>升级你的 ML 体验并获取预先训练的模型

如果你安装 SQL Server 2016 R Services 的早期版本，你可以现在升级到最新版本，通过切换服务器以使用现代的生命周期策略。 通过这样做，可以利用的更快的发行周期，并自动升级所有 R 组件。 有关详细信息，请参阅 [Microsoft R Server 9.0.1](https://docs.microsoft.com/r-server/whats-new-in-r-server)。

安装程序还提供了安装的预先训练的模型集合以二进制格式的选项。 在图像识别，所以可能很难客户若要查找大型数据集来训练某个模型等的情况下，这些模型支持机器学习。 安装的预先训练的模型之一后，你可以在自己而无需的时间和费用参与此类大型和复杂模型定型的数据进行预测使用它。

有关详细信息，请参阅[安装在 SQL Server 中预先训练的模型](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>管理包

此版本包括 SQL Server 的程序包管理中的许多改进。 其中包括：

- 数据库角色，以帮助 DBA 管理和审核权限
- 在 T-SQL 中创建 EXTERAL 库语句
- 一组丰富的 R 函数，来帮助安装，请删除，或列出用户拥有的包。

有关详细信息，请参阅[包管理](r/r-package-management-for-sql-server-r-services.md)。

### <a name="get-started"></a>要开始

+ [设置 SQL Server 计算机学习 Services 中的 Python](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [设置 SQL Server 计算机学习 Services 中的 R](r/set-up-sql-server-r-services-in-database.md)

+ [机器学习教程](tutorials/machine-learning-services-tutorials.md)
