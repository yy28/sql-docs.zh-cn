---
title: R 语言和 Python 脚本的扩展性体系结构
description: 对 SQL Server 数据库引擎的外部代码支持, 其中包含用于在关系数据上运行 R 和 Python 脚本的双体系结构。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a5c49172ed23867f95e383878f792092bd762177
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470459"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server 中的扩展性体系结构机器学习服务 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 具有可扩展性框架, 可用于在服务器上运行外部脚本, 例如 R 或 Python。 脚本在语言运行时环境中作为核心数据库引擎的扩展执行。 

## <a name="background"></a>背景

扩展性框架是 SQL Server 2016 中引入的, 用于支持 R 运行时。 SQL Server 2017 添加对 Python 的支持

扩展性框架的用途是在 SQL Server 和数据科学语言 (例如 R 和 Python) 之间提供一个接口, 以便在将数据科学解决方案移动到生产环境中时减少摩擦, 并保护开发期间公开的数据正在. 通过在 SQL Server 管理的安全框架中执行受信任的脚本语言, 数据库管理员可以保持安全性, 同时允许数据科学家访问企业数据。

下图直观地说明了可扩展体系结构的机会和优势。

  ![与 SQL Server 的集成目标](../media/ml-service-value-add.png "添加机器学习服务值")

任何 R 或 Python 脚本都可以通过调用存储过程来运行, 结果将作为表格结果直接返回 SQL Server, 这样就可以轻松地从任何可以发送 SQL 查询并处理结果的应用程序生成或使用机器学习。

+ 外部脚本执行受 SQL Server 的数据安全限制, 在这种情况下, 运行外部脚本的用户只能访问 SQL 查询中同样可用的数据。 如果查询因权限不足而失败, 则同一用户运行的脚本也会由于相同的原因而失败。 在表、数据库和实例级别实施 SQL Server 安全性。 数据库管理员可以管理用户访问权限、外部脚本使用的资源以及添加到服务器的外部代码库。  

+ 规模和优化机会有两种: 通过数据库平台 (列存储索引、[资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)) 和扩展特定的好处, 适用于适用于 R 和 Python 的 Microsoft 库用于数据科学模型。 R 是单线程的, RevoScaleR 函数是多线程的, 可以在多个内核之间分配工作负荷。

+ 部署使用 SQL Server 方法: 包装外部脚本的存储过程、嵌入的 SQL 或 T-sql 查询调用函数 (如预测) 可从保留在服务器上的预测模型返回结果。

+ 通过特定工具和 Ide 提供技能的 R 和 Python 开发人员可以在这些工具中编写代码, 然后通过端口代码来 SQL Server。

## <a name="architecture-diagram"></a>体系结构关系图

该体系结构的设计使外接程序可在与 SQL Server 不同的进程中运行, 但其组件由内部管理 SQL Server 的数据和操作请求链。 根据 SQL Server 的版本, 支持的语言扩展包括 R 和 Python。 

  ![组件体系结构](../media/generic-architecture.png "组件体系结构")

组件包括一个启动**板**服务, 用于调用特定于语言的启动器 (R 或 Python)、语言和特定于库的逻辑来加载解释器和库。 启动器会加载语言运行时间以及任何专有模块。 例如, 如果你的代码包含 RevoScaleR 函数, 则会加载 RevoScaleR 解释器。 **BxlServer**和**SQL 附属**项通过 SQL Server 管理通信和数据传输。

<a name="launchpad"></a>

## <a name="launchpad"></a>启动板

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是一项服务, 可管理和执行外部脚本, 这与全文索引和查询服务启动单独的主机用于处理全文查询的方式类似。 快速启动板服务只能启动由 Microsoft 发布的受信任的启动器, 或已由 Microsoft 认证为满足性能和资源管理要求的启动器。

| 受信任启动器 | 扩展名 | SQL Server 版本 |
|-------------------|-----------|---------------------|
| R 语言的 RLauncher | [R 扩展](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| 用于 Python 3.5 的 Pythonlauncher | [Python 扩展](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务在其自身的用户帐户下运行。 如果更改运行快速启动板的帐户, 请务必使用 SQL Server 配置管理器执行此操作, 以确保将更改写入相关文件。

为已[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]添加到 SQL Server 机器学习服务的每个数据库引擎实例创建一个单独的服务。 每个数据库引擎实例都有一个启动板服务, 因此, 如果有多个具有外部脚本支持的实例, 则每个实例都有一个启动板服务。 数据库引擎实例将绑定到为其创建的启动板服务。 存储过程或 T-sql 中的外部脚本的所有调用都将导致 SQL Server 服务调用为同一实例创建的快速启动板服务。

若要以特定支持的语言执行任务, 快速启动板将从池中获取一个安全的工作线程帐户, 并启动一个用于管理外部运行时的附属进程。 每个附属进程都将继承快速启动板的用户帐户, 并在脚本执行期间使用该工作线程帐户。 如果脚本使用并行进程, 则会在同一单个辅助角色帐户下创建它们。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 附属项

**BxlServer**是由 Microsoft 提供的可执行文件, 用于管理 SQL Server 与 Python 或 R 之间的通信。它创建用于包含外部脚本会话的 Windows 作业对象, 为每个外部脚本作业预配安全工作文件夹, 并使用 SQL 附属项管理外部运行时和 SQL Server 之间的数据传输。 如果在作业运行时运行[进程资源管理器](https://technet.microsoft.com/sysinternals/processexplorer.aspx), 则可能会看到一个或多个 BxlServer 实例。

实际上, BxlServer 是与用于传输数据和管理任务的 SQL Server 语言运行时环境的配套。 BXL 代表二进制交换语言, 是指用于在 SQL Server 和外部进程之间有效移动数据的数据格式。 BxlServer 也是相关产品 (如 Microsoft R Client 和 Microsoft R Server) 的重要组成部分。

**SQL 附属**项是一个可扩展 API, 它包含在从 SQL Server 2016 开始的数据库引擎中, 支持使用 C 或C++实现的外部代码或外部运行时。

BxlServer 使用 SQL Satellite 执行以下任务：

+ 读取输入数据
+ 写入输出数据
+ 获取输入参数
+ 写入输出参数
+ 错误处理
+ 将 STDOUT 和 STDERR 写回客户端

SQL 附属项使用一种自定义数据格式, 该格式经过优化, 可用于在 SQL Server 和外部脚本语言之间进行快速数据传输。 它在 SQL Server 与外部脚本运行时之间的通信过程中执行类型转换, 并定义输入和输出数据集的架构。

可以使用 windows 扩展事件 (xEvents) 监视 SQL 附属项。 有关详细信息, 请参阅[适用于 R 的扩展事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)和[Python 的扩展事件](../../advanced-analytics/python/extended-events-for-python.md)。

## <a name="communication-channels-between-components"></a>组件之间的通信通道

本节介绍了组件和数据平台之间的通信协议。

+ **TCP/IP**

  默认情况下, SQL Server 与 SQL 附属项之间的内部通信使用 TCP/IP。

+ **命名管道**

  BxlServer 和 SQL Server 到 SQL 附属项之间的内部数据传输使用专用的压缩数据格式来增强性能。 使用命名管道在语言运行时间和 BXL 格式的 BxlServer 之间交换数据。

+ **ODBC**

  外部数据科学客户端与远程 SQL Server 实例之间的通信使用 ODBC。 将脚本作业发送到 SQL Server 的帐户必须具有连接到该实例和运行外部脚本所需的两个权限。

  此外, 根据任务的不同, 帐户可能需要以下权限:

  + 读取作业使用的数据
  + 将数据写入表: 例如, 将结果保存到表中
  + 创建数据库对象: 例如, 如果将外部脚本保存为新存储过程的一部分, 则为。

  当 SQL Server 用作从远程客户端执行的脚本的计算上下文时, 并且可执行文件必须从外部源检索数据时, ODBC 将用于写回。 SQL Server 将发出远程命令的用户的标识映射到当前实例上用户的标识, 并使用该用户的凭据运行 ODBC 命令。 执行此 ODBC 调用所需的连接字符串从客户端代码中获取。

+ **RODBC (仅限 R)** 

  可以使用 **RODBC** 在脚本内部发出其他 ODBC 调用。 RODBC 是一种常用的 R 包, 用于访问关系数据库中的数据;但是, 它的性能通常比 SQL Server 使用的同类提供程序速度慢。 许多 R 脚本使用 RODBC 的嵌入式调用，类似于检索用于分析的“辅助”数据集。 例如，用于训练模型的存储过程可以定义一个 SQL 查询来获取用于训练模型的数据，但使用嵌入式 RODBC 调用来获取其他因子，以执行查找，或者从文本文件或 Excel 等外部源中获取新数据。

  以下代码演示了 R 脚本中嵌入的 RODBC 调用：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他协议**

  可能需要在 "区块" 中工作或将数据传输回远程客户端的过程也可以使用[XDF 文件格式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 实际数据传输通过编码的 blob。

## <a name="see-also"></a>请参阅

+ [SQL Server 中的 R 扩展](extension-r.md)
+ [SQL Server 中的 Python 扩展](extension-python.md)