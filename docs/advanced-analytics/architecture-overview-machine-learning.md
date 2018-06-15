---
title: 对 SQL Server 机器学习服务的体系结构概述 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4abe5e508f1e183e1e6cb5012b9541fe3723b77a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202980"
---
# <a name="architecture-overview-for-sql-server-machine-learning-services"></a>对 SQL Server 机器学习服务的体系结构概述 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本指南介绍了在 SQL Server 中支持的 Python 和 R 脚本执行的 extensibility framework 的目标。

它还提供概述如何设计体系结构以满足这些目标，如何 R 和 Python 支持和执行的 SQL Server 和集成的好处。

总体上而言的扩展性框架是几乎完全相同的 R 和 Python，称为启动器的详细信息，配置选项和等一些细微的差别。 有关特定语言的实现详细信息，请参阅这些文章：

- [SQL Server R Services 的体系结构概述](r/architecture-overview-sql-server-r.md)
- [SQL Server 中的 Python 的体系结构概述](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>背景

SQL Server 2016 数据库引擎，以支持使用 SQL Server 的 R 脚本执行引入了大量的更改。 在 SQL Server 自 2017 年，此基础结构已经过改进，若要添加的 Python 语言的支持。

扩展性框架的目标是创建 SQL Server 和数据科学语言，如 R 和 Python，同时可以减少数据科学解决方案移到生产环境，时发生的摩擦并保护可能的数据之间的更好接口公开在数据科学开发过程中。

通过执行由 SQL Server 管理的安全框架内的受信任的脚本语言，数据库开发人员可以保持安全，同时允许数据科学家使用企业数据。

  ![与 SQL Server 的集成的目标](media/ml-service-value-add.png "机器学习服务值添加")

- R 或 Python 的当前用户应该能够端口其代码，以及执行其在 SQL Server 中相对较小的修改。
- SQL Server 中的数据安全模型已经扩展到了外部脚本语言使用的数据。 换而言之，有人运行 R 或 Python 脚本应不能使用 SQL 查询中的该用户无法访问的任何数据。
- 数据库管理员应该能够管理所使用的外部脚本资源、 管理用户，和管理和监视外部的代码库。
- 系统必须支持基于开放源代码 R 和 Python，但使用专有组件开发的分发上完全由 Microsoft 提供更高的安全和性能的解决方案。

## <a name="architecture-core-concepts"></a>体系结构的核心概念

为了满足这些目标，SQL Server 2016 R Services 和 SQL Server 自 2017 年 1 机器学习 Services R 和 Python 的体系结构基于这些核心概念：

+ **多进程体系结构**

  R 和 Python 都是具有丰富且热情社区支持的开放源代码语言。 因此，务必维护使用开放源代码 R 和 Python 的完全互操作性。

  R 和 Python 的开放源代码分发许可，与 SQL Server 安装和独立从 SQL Server 可以运行必要。

   此外，Microsoft 提供了一组提供与 SQL Server，包括数据转换、 压缩和优化针对每个受支持的语言集成的专有库。

+ **安全性**

   更佳的安全性意味着支持集成的 Windows 身份验证和基于密码的 SQL 登录名，作为凭据，也为安全处理进行数据保护和使用 SQL Server 受信任的快速启动板来管理外部脚本需依赖于 SQL Server执行和在脚本中使用的安全数据。

+ **可伸缩性和性能**

  与 SQL Server 的集成是于改进企业中的 R 和 Python 的用途的密钥。 可以通过调用存储的过程中，运行任何 R 或 Python 脚本和结果返回为表格结果直接到 SQL Server，从而便于生成或使用从任何应用程序能够发送 SQL 查询和处理结果的机器学习。

  性能优化依赖于平台的两个同样功能强大的方面： 资源调控和并行处理使用 SQL Server 和分布式计算算法提供**RevoScaleR**和**revoscalepy**。

## <a name="solution-development-and-deployment"></a>解决方案开发和部署

除了扩展性平台这些核心目标，SQL Server 中的机器学习服务旨在提供强集成与数据库引擎的 BI 堆栈，这些优势：

+ 通过传统的监视工具的性能和资源管理
+ 易于使用的 Python 和 R 数据通过 BI 套件或任何应用程序可以使用 SQL 查询结果
+ 用于的计算机学习解决方案的企业开发多较低屏障

让我们查看其在实践中的工作方式。

  ![ML 解决方案开发过程](media/ml-solution-development-process.png "开发和部署使用机器学习服务")

1. 数据保存在法规遵从性的边界内，并且可以管理和监视 SQL server 数据的使用。 同时，DBA 可以完全控制谁可以安装包或在服务器上运行脚本。 如果需要的话，DBA 还可以委派到数据科学家或管理器数据库级别权限。
2. 数据科学家可以生成和测试解决方案，在其首选 R 或 Python 环境中，与服务器断开连接。
3. SQL 开发人员可以使用熟悉的工具，例如 Management Studio 或 Visual Studio 将与 SQL Server 集成的 R 或 Python 代码。 紧密集成意味着知识的开发人员可以选择以优化每个任务的最佳工具。 例如，可以使用某些功能工程任务和 R SQL 其他人。 你可能在 Integration Services 任务执行复杂的文本分析中嵌入 Python 脚本。
4. 可以使用 SQL Server 技术，例如列存储索引、 更好的性能优化测试和准备就绪，可以向部署的解决方案。 较新的功能允许你批处理训练并行对分区的数据集的多个小模型或评分中使用针对机器学习任务进行了优化的本机 SQL 代码的行数以百万计。
5. 已准备好脱离？ 通过使用存储的过程，您可以轻松地公开预测的 BI 堆栈或外部的应用程序解决方案。

## <a name="related-products"></a>相关的产品

无法确定哪台计算机学习解决方案满足你的需求？ 除了 SQL Server 2016 和 SQL Server 自 2017 年中的嵌入分析，Microsoft 提供以下机器学习平台和服务：

+ [Microsoft R Server 和机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)

  用于开发、 分发和管理机器学习作业的多平台环境
+ [数据科学虚拟机](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  需要机学习、 预装的所有工具。 使用 Jupyter 笔记本、 Python 或。
  
  尝试新[Windows 2016 预览版本](http://aka.ms/dsvm/win2016)，其中包括常用深入学习框架，例如 CNTK 和 mxNet，以及为 Windows 容器支持的 GPU 版本 ！

+ [Azure 的认知服务](https://azure.microsoft.com/services/cognitive-services/)

  各种云服务集成到应用程序，包括视频、 面部识别的自然语言索引添加 AI 和 ML 表情检测，文本分析计算机转换过程中，和很多，更
+ [Azure 机器学习](https://azure.microsoft.com/services/machine-learning/)

  基于云的拖放接口设计机器学习工作流，结合了能够自动执行和与通过 web 服务和 PowerShell 的应用程序集成

## <a name="see-also"></a>另请参阅

[比较机器学习服务器和 Microsoft R 产品](https://docs.microsoft.com/machine-learning-server/what-is-r-server-interoperability)
