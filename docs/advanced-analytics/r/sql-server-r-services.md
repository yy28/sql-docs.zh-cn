---
title: SQL Server 2016 中的 R Services |Microsoft Docs
description: 概述介绍了 SQL Server 服务，对数据库内分析 R 的支持
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/27/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8874c7196e77e9df7fe710f1b02be49cee10e3c8
ms.sourcegitcommit: 010755e6719d0cb89acb34d03c9511c608dd6c36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240093"
---
# <a name="r-services-in-sql-server-2016"></a>SQL Server 2016 中的 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2016 R Services 是用于 SQL 服务器上执行 R 代码和函数的数据库引擎实例的附加内容。 独立于核心引擎进程，但完全可用于关系数据作为存储过程、 包含 R 语句的 T-SQL 脚本或包含 T-SQL 的 R 代码，代码中的可扩展性框架，运行。 

R Services 包括基本分发，，上面有来自 Microsoft 的企业 R 包，以便可以加载和处理大量数据的多个核心上并聚合到单个合并输出结果。 Microsoft 的 R 函数和算法设计规模和实用程序： 提供预测分析、 统计建模、 数据可视化效果和先进的机器学习算法中设计商业服务器产品和由 Microsoft 支持。 

R 库包括 RevoScaleR、 MicrosoftML，和其他人。 因为与数据库引擎集成 R Services，可以让分析贴近数据，并消除成本和与数据移动相关的安全风险。

## <a name="components"></a>组件

SQL Server 2016 仅为 R。 下表介绍了 SQL Server 2016 中的功能。

| 组件 | Description |
|-----------|-------------|
| SQL Server 快速启动板服务 | 用于管理外部 R 运行时和 SQL Server 实例之间的通信的服务。 |
| R 包 | [**RevoScaleR** ](revoscaler-overview.md)是主库的此库中的可缩放。 函数是最广泛使用。 这些库中找到数据转换和操作、 统计汇总、 可视化和建模和分析多种形式。 此外，这些库中的函数会自动将工作负荷分散到以便并行处理，能够工作的协调和管理计算引擎的数据块上的可用内核。  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)添加机器学习算法来创建自定义文本分析、 图像分析和情绪分析模型。 <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)用于 R 脚本置于 T-SQL 存储过程、 向数据库注册存储的过程和从 R 开发环境运行存储的过程提供帮助器函数。<br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md)用于在 R 中指定的 MDX 查询|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open)是 Microsoft 的开放源代码分发的。包含包和解释器。 始终使用 MRO 由安装程序安装的版本。 |
| R 工具 | R 控制台窗口和命令提示中的 R 分发版的标准工具。  |
| R 示例和脚本 |  开放源代码 R 和 RevoScaleR 包包括内置的数据集，以便您可以创建和运行脚本使用预安装的数据 |
| 在 R 中预先训练的模型 | 预先训练的模型创建的特定用例和在 Microsoft 数据科学工程团队维护的。 可以使用预先训练的模型作为-是正负情绪评分中的文本，或在映像中，使用你提供的新数据输入检测功能。 模型在 R Services 中运行，但不能通过 SQL Server 安装程序安装。 有关详细信息，请参阅[安装预先定型的机器学习模型的 SQL Server](../install/sql-pretrained-models-install.md)。 |

## <a name="using-r-services"></a>使用 R Services

开发人员和分析师通常具有在本地 SQL Server 实例上运行的代码。 可以通过添加机器学习服务并启用外部脚本执行，在 SQL 服务器模式中运行 R 代码的能力： 存储过程中包装脚本、 存储模型中的 SQL Server 表，或结合查询中的 T-SQL 和 R 函数。

数据库内分析的最常见方法是使用[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，Rscript 传递作为输入参数。

经典的客户端-服务器交互是另一种方法。 从任何客户端工作站上具有一个 IDE，可以安装[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)，然后编写将推送执行的代码 (称为*远程计算上下文*) 对数据和到远程 SQL 操作服务器。 

最后，如果使用的[独立服务器](r-server-standalone.md)和 Developer edition 中，你可以构建解决方案，客户端工作站上使用相同的库和解释器，并随后部署生产代码中的对 SQL Server 机器学习服务 （数据库内）。 

## <a name="how-to-get-started"></a>如何开始

开始安装程序，将二进制文件附加到您最喜欢的开发工具，编写第一个脚本。

**步骤 1:** 安装和配置软件。 

+ [安装 SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)

**步骤 2:** 获得亲身体验，使用这些教程之一：

+ [教程： 了解使用 R 的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [教程： 使用 R 的端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**步骤 3:** 添加你最喜欢的 R 程序包并使用它们以及由 Microsoft 提供的包

+ [SQL Server 的 R 包管理](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>另请参阅

 [安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
