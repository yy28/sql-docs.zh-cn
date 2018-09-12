---
title: SQL Server 机器学习服务中的可扩展性体系结构 |Microsoft Docs
description: 外部代码支持的 SQL Server 数据库引擎，使用双体系结构的关系数据上运行 R 和 Python 脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fae8beb4f865c537f00fa8b58a01cafe09541d71
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892854"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>SQL Server 机器学习服务中的可扩展性体系结构 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 具有可扩展性框架，用于在服务器上运行 R 或 Python 等外部脚本。 作为核心数据库引擎的扩展的语言运行时环境中执行脚本。 

## <a name="background"></a>背景

SQL Server 2016 支持 R 运行时中引入了可扩展性框架。 SQL Server 2017 添加了对 Python 支持

可扩展性框架的用途是提供 SQL Server 和 R 和 Python，移动到生产环境，并保护数据的数据科学解决方案公开在开发过程时减少冲突等的数据科学语言之间的接口过程。 通过执行由 SQL Server 管理的安全框架中受信任的脚本语言，数据库管理员可以在允许访问企业数据的数据科学家时保持安全。

下图以可视化方式描述机会和可扩展的体系结构的优点。

  ![与 SQL Server 集成的目标](../media/ml-service-value-add.png "机器学习服务值添加")

可以通过调用存储的过程，运行任何 R 或 Python 脚本和结果作为表格结果直接返回到 SQL Server，使其可以轻松地生成或使用机器学习从任何应用程序可发送的 SQL 查询和处理结果。

+ 外部脚本执行受到 SQL Server 数据安全性，其中运行外部脚本的用户可以仅访问同样可在 SQL 查询中的数据。 如果查询因权限不足，也会出于相同原因失败由同一用户运行的脚本。 SQL Server 安全性是在表、 数据库和实例级别强制实施。 数据库管理员可以管理用户的访问权限、 使用的外部脚本、 资源和添加到服务器的外部代码库。  

+ 缩放和优化机会有了双： 通过数据库平台提高 (列存储索引[资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md))，和特定于扩展的提升对 R 和 Python 的 Microsoft 库用于数据时科学模型。 R 是单线程，RevoScaleR 函数是多线程、 能够将工作负荷分布在多个内核。

+ 部署使用 SQL Server 方法： 包装外部脚本的存储过程，嵌入 SQL 或 T-SQL 查询返回的服务器上保持结果从预测模型的预测等的调用函数。

+ R 和 Python 开发人员提供建立的特定工具和 Ide 的技能可在这些工具中编写代码，然后代码移植到 SQL Server。

## <a name="architecture-diagram"></a>体系结构关系图

体系结构设计为在单独进程中运行的外部脚本，从 SQL Server，但与在内部管理对数据和 SQL 服务器上的操作请求的链的组件。 具体取决于 SQL Server 的版本，支持的语言扩展包括 R 和 Python。 

  ![组件体系结构](../media/generic-architecture.png "组件体系结构")

组件包括**快速启动板**服务用来调用特定于语言的启动器 （R 或 Python），语言和特定于库的逻辑，用于加载解释器和库。 启动器加载语言中运行的时间，加上任何专有的模块。 例如，如果你的代码包括 RevoScaleR 函数，会加载 RevoScaleR 解释器。 **BxlServer**并**SQL Satellite**管理与 SQL Server 的通信和数据传输。

## <a name="launchpad"></a>启动板

SQL Server Trusted Launchpad 是一种服务，管理和执行外部脚本，类似于全文索引和查询服务用于处理全文查询启动单独的主机的方式。 快速启动板服务可以开始仅受信任的启动器，均由 Microsoft、 或的具有已经 Microsoft 认证满足性能和资源管理的要求。

| 受信任的启动器 | 扩展名 | SQL Server 版本 |
|-------------------|-----------|---------------------|
| R 语言 RLauncher.dll | [R 扩展](extension-r.md) | SQL Server 2016 和 SQL Server 2017 |
| 适用于 Python 3.5 Pythonlauncher.dll | [Python 扩展](extension-python.md) | SQL Server 2017 |

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务在其自身的用户帐户下运行。 如果您更改运行 Launchpad 的帐户，请确保要执行此操作使用 SQL Server 配置管理器，以确保更改将写入相关文件。

若要执行的任务特定的受支持语言，快速启动板从池中获取受保护的辅助角色帐户，并启动一个附属过程来管理外部运行时。 每个附属进程继承的快速启动板的用户帐户，并执行脚本的持续时间内使用该辅助角色帐户。 如果脚本使用并行进程，则会创建相同的单个辅助角色帐户下。

## <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL Satellite

**BxlServer**是由 Microsoft 管理 SQL 服务器和 Python 或。 之间的通信提供可执行文件它创建 Windows 作业对象，用于包含外部脚本的会话，预配的安全工作文件夹的每个外部脚本作业，并使用 SQL Satellite 来管理外部运行时和 SQL Server 之间的数据传输。 如果在运行[Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx)运行作业时，可能会看到 BxlServer 的一个或多个实例。

实际上，BxlServer 是一种语言运行时环境，适用于 SQL Server 传输数据和管理任务的助手。 BXL 是二进制交换语言的缩写，是指使用 SQL Server 和外部进程之间有效移动数据的数据格式。 BxlServer 也是相关的产品，例如 Microsoft R Client 和 Microsoft R Server 的一个重要部分。

**SQL Satellite**是扩展性 API，包括在数据库引擎从 SQL Server 2016，支持外部代码开始或使用 C 或 c + + 实现的外部运行时。

BxlServer 使用 SQL Satellite 执行以下任务：

+ 读取输入数据
+ 写入输出数据
+ 获取输入参数
+ 写入输出参数
+ 错误处理
+ 将 STDOUT 和 STDERR 写回客户端

SQL Satellite 使用 SQL Server 和外部脚本语言之间的快速数据传输进行了优化的自定义数据格式。 它执行类型转换，并在 SQL Server 和外部脚本运行时之间的通信过程定义输入和输出数据集的架构。

可以通过使用 windows 扩展事件 (xEvents) 监视 SQL Satellite。 有关详细信息，请参阅[适用于 R 的扩展事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)并[适用于 Python 的扩展事件](../../advanced-analytics/python/extended-events-for-python.md)。

## <a name="communication-channels-between-components"></a>组件之间的通信通道

在本部分中描述了组件和数据平台之间的通信协议。

+ **TCP/IP**

  默认情况下，SQL Server 和 SQL Satellite 之间的内部通信使用 TCP/IP。

+ **命名管道**

  BxlServer 和 SQL Server 通过 SQL Satellite 之间的内部数据传输使用专有的压缩数据格式来增强性能。 BXL 格式，使用命名管道语言运行时间和 BxlServer 之间交换数据。

+ **ODBC**

  外部数据科学客户端和远程 SQL Server 实例之间的通信使用 ODBC。 将脚本的作业发送到 SQL Server 的帐户必须具有这两个权限才能连接到的实例并运行外部脚本。

  此外，具体取决于任务，该帐户可能需要这些权限：

  + 读取作业使用的数据
  + 将数据写入到表： 例如，保存结果到表
  + 创建数据库对象： 例如，如果将外部脚本另存为新的存储过程的一部分。

  当 SQL Server 用作计算上下文中执行脚本时远程客户端，并可执行文件必须从外部源检索数据，ODBC 将用于写回。 SQL Server 映射到当前实例上的用户的标识发出远程命令的用户的标识，并运行 ODBC 命令使用该用户的凭据。 执行此 ODBC 调用所需的连接字符串从客户端代码中获取。

+ **RODBC (仅适用于 R)** 

  可以使用 **RODBC** 在脚本内部发出其他 ODBC 调用。 RODBC 是用于访问关系数据库; 中的数据的流行 R 包但是，其性能低于通常可比较使用的 SQL Server 的提供程序。 许多 R 脚本使用 RODBC 的嵌入式调用，类似于检索用于分析的“辅助”数据集。 例如，用于训练模型的存储过程可以定义一个 SQL 查询来获取用于训练模型的数据，但使用嵌入式 RODBC 调用来获取其他因子，以执行查找，或者从文本文件或 Excel 等外部源中获取新数据。

  以下代码演示了 R 脚本中嵌入的 RODBC 调用：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他协议**

  在"块"中工作或者将数据传回给远程客户端可能需要的进程还可以使用[XDF 文件格式](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 实际数据传输均通过编码的 blob。

## <a name="see-also"></a>请参阅

+ [SQL Server 中的 R 扩展](extension-r.md)
+ [SQL Server 中的 Python 扩展](extension-python.md)