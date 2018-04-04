---
title: SQL Server 中的支持 R 组件 |Microsoft 文档
ms.custom: ''
ms.date: 04/05/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: cc9f600d6bfce5d522abb8452800c35f41069b92
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="components-in-sql-server-to-support-r"></a>SQL Server 中支持 R 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在 SQL Server 2016 和自 2017 年中，数据库引擎包括支持对外部脚本语言，包括 R 和 Python 的可扩展性的可选组件。 SQL Server 2016; 中添加了对 R 语言支持对 SQL Server 自 2017 年 1 机器学习 Services 中添加 Python 的支持。

本主题描述专门用于 R 语言的新组件。 有关这些组件如何使用开放源代码 R 的讨论，请参阅[R 互操作性](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>组件和提供程序

除了用于加载 R 和执行 R 代码的 shell（请参阅体系结构概述）以外，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 还包含以下附加组件。

### <a name="launchpad"></a>启动板 

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是由提供的服务[!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)]支持的外部脚本，类似于全文索引和查询服务用于处理全文查询启动单独的主机的方式执行。

Launchpad 服务只会启动 Microsoft 发布的受信任启动器，或者经 Microsoft 认证满足性能和资源管理要求的启动器。 特定于语言的启动器的命名非常简单：

  + R -  RLauncher.dll
  + Python-PythonLauncher.dll

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务在其自身的用户帐户下运行。 特定语言运行时的每个附属进程将继承 Launchpad 的用户帐户。 有关配置和快速启动板的安全上下文的详细信息，请参阅[安全概述](../../advanced-analytics/r/security-overview-sql-server-r.md)。

### <a name="bxlserver-and-sql-satellite"></a>BxlServer 和 SQL 卫星

BxlServer 是由 Microsoft 管理之间的通信提供可执行文件[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]以及 R 运行时和还实现 RevoScaleR 函数。 它可以创建用于包含 R 会话的 Windows 作业对象、预配每个 R 作业的安全工作文件夹，并使用 SQL Satellite 来管理 R 与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之间的数据传输。

实际上，BxlServer 是 R 的伴侣组件，可使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 来支持 R 与 SQL Server 的集成。 BXL 是二进制 Exchange 语言的缩写，指使用如当你安装 Microsoft R 客户端或 Microsoft R Server，也会安装。 BxlServer.dll 高效地移动 SQL Server 和外部进程之间的数据的数据格式。

SQL Satellite 是 SQL Server 2016 中由数据库引擎提供的新可扩展性 API，用于支持使用 C 或 C++ 实现的外部代码或外部运行时。 BxlServer 使用 SQL Satellite 来与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通信。

SQL Satellite 使用自定义数据格式，这种格式已针对 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 与外部脚本语言之间的快速数据传输进行优化。 在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 与 R 通信期间，SQL Satellite 将执行类型转换并定义输入和输出数据集的架构。

BxlServer 使用 SQL Satellite 执行以下任务：

  + 读取输入数据
  + 写入输出数据
  + 获取输入参数
  + 写入输出参数
  + 错误处理
  + 写入标准输出和错误返回到客户端

可以使用扩展事件监视 SQL Satellite。 有关详细信息，请参阅 [SQL Server R Services 的扩展事件](extended-events-for-sql-server-r-services.md)。

## <a name="communication-channels-between-components"></a>组件之间的通信通道

+ **TCP/IP**

    默认情况下，之间的内部通信[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和 SQL 附属使用 TCP/IP。

+ **命名管道**

    BxlServer 之间的内部数据传输和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]通过 SQL 附属使用专有的压缩数据格式以增强性能。 从 R 内存到 BxlServer 的数据通过 BXL 格式的命名管道交换。

+ **ODBC**

    外部数据科学客户端之间的通信和[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]实例使用 ODBC。 将 R 作业发送到 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的帐户必须有权连接到实例，同时有权运行外部脚本。 此外，该帐户必须有权访问作业使用的任何数据、写入数据（例如，如果将结果保存到表中），或创建数据库对象（例如，如果将 R 函数保存为新存储过程的一部分）。

    如果将 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 用作远程客户端发送的 R 作业的计算上下文，并且 R 命令必须从外部源检索数据，则 ODBC 将用于写回。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将发出远程 R 命令的用户标识映射到当前实例上的用户标识，并使用该用户的凭据运行 ODBC 命令。 执行此 ODBC 调用所需的连接字符串从客户端代码中获取。

    可以使用 **RODBC** 在脚本内部发出其他 ODBC 调用。 RODBC 是用于访问关系数据库中数据的流行 R 包；但是，与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用的同等提供程序相比，其性能通常较慢。 许多 R 脚本使用 RODBC 的嵌入式调用，类似于检索用于分析的“辅助”数据集。 例如，用于训练模型的存储过程可以定义一个 SQL 查询来获取用于训练模型的数据，但使用嵌入式 RODBC 调用来获取其他因子，以执行查找，或者从文本文件或 Excel 等外部源中获取新数据。

    以下代码演示了 R 脚本中嵌入的 RODBC 调用：

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **其他协议**

    此外可以使用"区块"中的工作或将数据传输回远程客户端可能需要的进程。支持的 Microsoft。 实际的数据传输的 XDF 格式是通过编码的 blob。

## <a name="interaction-of-components"></a>组件的交互

前面所述的组件体系结构保证开源 R 代码可“按原样”工作，同时大幅提升 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上运行的代码的性能。 根据 R 代码的启动方式，控制组件与 R 运行时和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎之间交互方式的机制有所不同。 本部分汇总了一些重要方案。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>从 SQL Server 数据库中执行 R 脚本

从 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]“内部”运行的 R 代码通过调用某个存储过程来执行。 因此，可以发出存储过程调用的任何应用程序都可以启动 R 代码的执行。  然后，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将按下图中概括的方式管理 R 代码的执行。

![rsql_indb780-01](media/script_in-db-r.png)

1. 对 R 运行时发出的请求由传递给存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的参数 _@language='R'_ 指示。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将此请求发送到 Launchpad 服务。
2. Launchpad 服务启动相应的启动器（在本例中为 RLauncher）。
3. RLauncher 启动外部 R 进程。
4. BxlServer 与 R 运行时协同工作，管理与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之间的数据交换并存储工作结果。
5. SQL 卫星管理相关任务有关的通信和处理[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer 使用 SQL Satellite 向 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 传递状态和结果。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 获取结果并关闭相关任务和进程。

### <a name="r-scripts-executed-from-a-remote-client"></a>从远程客户端执行 R 脚本

从支持 Microsoft R 远程数据科学客户端连接时，你可以在上下文中运行 R 函数[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]使用 RevoScaleR 函数。 此工作流与前面的工作流不同，下图对此做了汇总。

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. 对于 RevoScaleR 函数，R 运行时调用的链接的函数，后者反过来调用 BxlServer。
2. BxlServer 已随附在 Microsoft R 中，在独立于 R 运行时的进程中运行。
3. BxlServer 确定连接目标并使用 ODBC 发起连接，传递 R 数据源对象的连接字符串中提供的凭据。
4. BxlServer 打开与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例的连接。
5. 对于 R 调用，快速启动板调用服务，即打开启动了适当的启动器 RLauncher。 然后，R 代码的处理过程类似于从 T-SQL 运行 R 代码。
6. RLauncher 针对 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上安装的 R 运行时实例发出调用。
7. 将结果返回到 BxlServer。
8. SQL Satellite 管理与 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 之间的通信并清理相关的作业对象。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将结果传回客户端。

## <a name="next-steps"></a>后续步骤

[体系结构概述](architecture-overview-sql-server-r.md)

[安全性概述](security-overview-sql-server-r.md)

[安全注意事项](security-considerations-for-the-r-runtime-in-sql-server.md)
