---
title: "用于与 SQL Server 的 Python 集成组件 |Microsoft 文档"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 6f948473c51d6212d432ddb179d7a61fcfdef117
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="components-in-sql-server-to-support-python-integration"></a>在 SQL Server 以支持 Python 集成的组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

机器学习服务从 SQL Server 自 2017 年开始，支持作为一种外部的语言，可以从 T-SQL 的执行或远程作为计算上下文中使用 SQL Server 执行的 Python。

具体而言，本主题介绍中通常支持可扩展性的 SQL Server 2017 和 Python 语言的组件。

## <a name="sql-server-components-and-providers"></a>SQL Server 组件和提供程序

若要配置 SQL Server 自 2017 年 1 以允许执行 Python 脚本是一个多步骤过程。

1. 安装扩展性功能。
2. 启用外部脚本执行功能。
3. 重新启动数据库引擎服务。

可能需要其他步骤来支持远程脚本执行。

有关详细信息，请参阅[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](../install/sql-machine-learning-services-windows-install.md)。

### <a name="launchpad"></a>启动板

SQL Server 受信任的启动板是 SQL Server 2016 的管理并执行外部脚本，类似于全文索引和查询服务用于处理全文查询启动单独的主机的方式中引入的服务。

快速启动板服务可以启动，发布由 Microsoft、 或，以满足性能和资源管理的要求认证由 Microsoft 仅受信任启动程序。

+ SQL Server 2017 支持 R 和 Python 3.5
+ SQL Server 2016 支持 R

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务在其自身的用户帐户下运行。

> [!TIP]
> 如果你更改运行快速启动板的帐户，请务必执行操作，以便使用 SQL Server 配置管理器，以确保更改将写入相关文件。

若要在特定的受支持的语言中执行任务，快速启动板从该池，获取受保护的工作帐户，并启动一个附属过程来管理外部运行时：

+ R 语言 RLauncher.dll
+ For Python 3.5 Pythonlauncher.dll

每个附属进程继承的快速启动板的用户帐户，该工作帐户用于执行脚本的持续时间。 如果 Python 脚本使用并行进程，则会创建同一、 单一辅助帐户下。

快速启动板的安全上下文的详细信息，请参阅[安全](security-overview-sql-server-python-services.md)。

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 卫星

如果你运行[进程资源管理器](https://technet.microsoft.com/sysinternals/processexplorer.aspx)在 Python 作业运行时，你可能会看到 BxlServer 的一个或多个实例。

**BxlServer**是由 Microsoft 管理之间的通信提供可执行文件[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 Python （或 R）。 创建 Windows 作业对象，用于包含外部脚本会话，设置安全的工作文件夹，而对于每个外部脚本作业，并使用 SQL 附属来管理外部运行时之间的数据传输和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。

实际上，BxlServer 是一起提供适用于的 Python[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]可将数据传输和管理任务。 BXL 是二进制 Exchange 语言的缩写，并引用用于 SQL Server 和外部进程之间有效地移动数据的数据格式。 BxlServer 还有 Microsoft R 客户端和 Microsoft R Server 的一个重要部分。

**SQL 附属**是数据库引擎从 SQL Server 2016，支持外部代码开始中包括的扩展性 API 或使用 C 或 c + + 实现的外部运行时。

BxlServer 使用 SQL Satellite 执行以下任务：

+ 读取输入数据
+ 写入输出数据
+ 获取输入参数
+ 写入输出参数
+ 错误处理
+ 将 STDOUT 和 STDERR 写回客户端

SQL 附属使用自定义数据格式进行了优化的快速数据传输之间[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和外部脚本语言。 它执行类型转换，并在之间的通信期间定义的输入和输出数据集架构[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和外部脚本运行时。

可以使用 windows 扩展事件 (xEvents) 监视 SQL 附属。 有关详细信息，请参阅[Extended Events for R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)。

## <a name="communication-channels-between-components"></a>组件之间的通信通道

+ **TCP/IP**

  默认情况下，之间的内部通信[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 SQL 附属使用 TCP/IP。

+ **命名管道**

  BxlServer 与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之间通过 SQL Satellite 进行的内部数据传输使用专有的压缩数据格式来增强性能。 在使用命名管道的 BXL 格式 BxlServer 和 Python 之间交换数据。

+ **ODBC**

  外部数据科学客户端之间的通信和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]实例使用 ODBC。 会将脚本发送的帐户作业到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]必须具有两个权限才能连接到的实例并运行外部脚本。

  此外，具体取决于任务，该帐户可能需要这些权限：

  + 作业使用的读取数据
  + 将数据写入到表： 例如，保存结果到表
  + 创建数据库对象： 例如，如果将外部脚本另存为新的存储过程的一部分。

  当[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]是从远程客户端，执行 Python 脚本，Python 可执行文件必须从外部源中检索数据，请使用作为计算上下文，ODBC 用于写回。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 映射到在当前实例中，用户的标识发出远程命令的用户的标识，并运行使用该用户的凭据 ODBC 命令。 执行此 ODBC 调用所需的连接字符串从客户端代码中获取。

## <a name="interaction-of-components"></a>组件的交互

下图描绘了与每个受支持的方案的 Python 运行时 SQL Server 组件的交互： 从 Python 终端，使用 SQL Server 计算上下文中运行脚本，数据库和远程执行。

### <a name="python-scripts-executed-in-database"></a>执行 Python 脚本的数据库中

当你运行"内部"Python [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，必须将封装在特殊存储过程中，Python 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

已为存储过程中嵌入脚本后，任何应用程序可以调用存储的过程可以启动 Python 代码的执行。  此后[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]管理执行代码，如下图中进行了总结。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. 由参数指示 Python 运行时的请求`@language='Python'`传递给存储过程。 SQL Server 将此请求发送到快速启动板服务。
2. 在快速启动板服务启动了适当的启动器;在此情况下，PythonLauncher。
3. PythonLauncher 启动外部 Python35 进程。
4. BxlServer 协调与要管理的数据交换和工作结果的存储的 Python 运行时。
5. SQL 卫星管理相关任务有关的通信和处理[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer 使用 SQL Satellite 向 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 传递状态和结果。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 获取结果并关闭相关任务和进程。

### <a name="python-scripts-executed-from-a-remote-client"></a>从远程客户端执行的 Python 脚本

你可以从远程计算机，例如便携式计算机，运行 Python 脚本，并让他们的 SQl Server 计算机的上下文中执行，如果满足这些条件：

+ 相应地设计脚本
+ 远程计算机安装了机器学习服务所使用的扩展性库。 [Revoscalepy](what-is-revoscalepy.md)包是需要使用远程计算上下文。

从远程计算机发送脚本时下, 图总结了整个工作流。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 中支持的函数**revoscalepy**，Python 运行时调用的链接的函数，又会调用 BxlServer。
2. BxlServer 附带机器学习服务 （数据库），并在单独的进程中运行 Python 运行时中。
3. BxlServer 确定连接目标，并开始使用 ODBC，传递的 Python 脚本中的连接字符串的一部分提供的凭据的连接。
4. BxlServer 打开与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例的连接。
5. 当调用时的外部脚本运行时，调用该快速启动板服务，以又启动了适当的启动器： 在此情况下，PythonLauncher.dll。 此后，处理的 Python 代码处理类似于工作流中时从 T-SQL 中的存储过程调用 Python 代码。
6. PythonLauncher 调用的实例安装 Python[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]计算机。
7. 将结果返回到 BxlServer。
8. SQL Satellite 管理与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之间的通信并清理相关的作业对象。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将结果传回客户端。

## <a name="next-steps"></a>后续步骤

[SQL Server 中的 Python 的体系结构概述](architecture-overview-sql-server-python.md)
