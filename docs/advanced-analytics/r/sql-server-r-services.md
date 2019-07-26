---
title: SQL Server 2016 中的 R Services
description: 对关系数据，包括数据科学和统计建模和预测分析、 数据可视化等集成的 R 任务的 SQL Server 中的 R。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 32487d8c1a6c87c9ad916e4cfd517f9ba4cba6e2
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469910"
---
# <a name="r-services-in-sql-server-2016"></a>SQL Server 2016 中的 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services 是 SQL Server 2016 数据库引擎实例的附加组件，用于在 SQL Server 上执行 R 代码和函数。 代码在可扩展性框架中运行（与核心引擎进程隔离），但可作为存储过程、包含 R 语句的 T-SQL 脚本或包含 T-SQL 的 R 代码，此时完全适用于关系数据。 

R Services 包括 R 的基本分发，与 Microsoft 的企业 R 包重叠，以便你可以加载和处理多个核心上的大量数据，并将结果聚合成一个统一输出。 Microsoft 的 R 函数和算法专为规模和实用性而设计：在 Microsoft 设计和支持的商业服务器产品中提供预测分析、统计建模、数据可视化功能和领先的机器学习算法。 

R 库包括[**RevoScaleR**](ref-r-revoscaler.md)、 [**MicrosoftML (R)** ](ref-r-microsoftml.md)和其他。 由于 R Services 与数据库引擎集成，你可以使分析与数据位于较近的位置，并消除与数据移动相关的成本和安全风险。

> [!Note]
> R Services 在 SQL Server 2017 及更高版本中已重命名为[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md), 反映了 Python 的添加。

## <a name="components"></a>组件

SQL Server 2016 仅适用于 R。 下表介绍了 SQL Server 2016 中的功能。

| 组件 | Description |
|-----------|-------------|
| SQL Server 快速启动板服务 | 用于管理外部 R 运行时和 SQL Server 实例之间的通信的服务。 |
| R 包 | [**RevoScaleR**](ref-r-revoscaler.md)是主库的此库中的可缩放。此库中的函数是使用最广泛的函数。 在这些库中可以找到数据转换和操作、统计摘要、可视化以及许多形式的建模和分析。 此外，这些库中的函数可自动在可用内核之间分配工作负荷以进行并行处理，并且能够处理由计算引擎协调和管理的数据块。  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md)添加了机器学习算法，用于创建用于文本分析、图像分析和情绪分析的自定义模型。 <br/>[**sqlRUtils** ](ref-r-sqlrutils.md)供了辅助函数，用于将R脚本放入T-SQL存储过程、向数据库注册存储过程以及从R开发环境中运行存储过程。<br/>[**olapR** ](ref-r-olapr.md)用于在 R 中指定的 MDX 查询|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) 是 Microsoft 提供的 R 的开源分发版。其中包括包和解释器。 请始终使用安装程序安装的 MRO 版本。 |
| R 工具 | R 控制台窗口和命令提示符是 R 分发版中的标准工具。  |
| R 示例和脚本 |  开源 R 和 RevoScaleR 包中包括内置数据集，以便你可以使用预安装的数据来创建和运行脚本 |
| 在 R 中预先训练的模型 | 预先训练的模型为特定用例创建，由 Microsoft 的数据科学工程团队维护。 可以按原样使用预先训练的模型对文本中的积极/消极情绪进行评分，或者使用你提供的新数据输入检测图像中的特征。 这些模型在 R 服务中运行，但不能通过 SQL Server 安装程序安装。 有关详细信息，请参阅[在 SQL Server 上安装预先训练的机器学习模型](../install/sql-pretrained-models-install.md)。 |

## <a name="using-r-services"></a>使用 R Services

开发人员和分析师通常具有在本地 SQL Server 实例上运行的代码。 可以通过添加机器学习服务并启用外部脚本执行，在 SQL 服务器模式中运行 R 代码的能力： 存储过程中包装脚本、 存储模型中的 SQL Server 表，或结合查询中的 T-SQL 和 R 函数。

数据库内分析的最常见方法是使用[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，将 R 脚本作为输入参数传递。

经典的客户端-服务器交互是另一种方法。 在具有 IDE 的任何客户端工作站中，可以安装[Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)，然后编写代码，将执行（称为“远程计算上下文”）推送到数据，以及将操作推送到远程 SQL 服务器。 

最后，如果使用的是[独立服务器](r-server-standalone.md)和 Developer Edition，则可以使用相同的库和解释器在客户端工作站上构建解决方案，然后在 SQL Server 机器学习服务（数据库中）上部署生产代码。 

## <a name="how-to-get-started"></a>如何开始

从安装开始，将二进制文件附加到您最喜欢的开发工具上，并编写第一个脚本。

**步骤 1：** 安装和配置软件。 

+ [安装 SQL Server 2016 R Services （数据库内）](../install/sql-r-services-windows-install.md)

**步骤 2：** 使用以下任一教程获取动手体验:

+ [教程：使用 R 了解数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [教程：带有 R 的端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**步骤 3：** 添加你最喜欢的 R 包, 并将其与 Microsoft 提供的包结合使用

+ [SQL Server 的 R 包管理](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>请参阅

 [安装 SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
