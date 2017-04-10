---
title: "SQL Server 以支持 R 服务中的新组件 | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# SQL Server 以支持 R 服务中的新组件

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 包括新组件，由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎，R 语言支持可扩展性。 这些组件的安全性由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和将在下文中详细信息。

## 新的 SQL Server 组件和提供程序

除了加载 R 和体系结构概述中所述执行的 R 代码的 shell [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 包括这些附加组件。

### **快速启动板** 
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 是由提供的新服务 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] 支持执行外部脚本，类似于全文索引和查询服务用于处理全文查询启动单独的主机的方式。 
  
  快速启动板服务将启动仅受信任的启动器，由 Microsoft、 发布或，为满足性能和资源管理的要求认证由 Microsoft。 在 [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], ，R 是当前支持的唯一外部语言 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]。
  
   [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 服务在其自己的用户帐户下运行。 为特定语言运行时每个附属进程将继承快速启动板的用户的帐户。 有关配置和快速启动板的安全上下文的详细信息，请参阅 [安全概述](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)。

### **BxlServer 和 SQL 附属**
  BxlServer 是由 Microsoft 管理之间的通信提供的可执行文件 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和 R 运行时以及实现 ScaleR 函数。 创建 Windows 作业对象，用于包含 R 会话、 设置安全的工作文件夹，而对于每个 R 作业，并使用 SQL 附属来管理 R 之间的数据传输和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  

  实际上，BxlServer 是适用于的 R 的配套 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 来支持的 R 随 SQL Server 的集成。 BXL 是二进制 Exchange 语言的缩写，是指用于 SQL Server 和 R.等外部进程进程之间有效地移动数据的数据格式 

 SQL 附属是由数据库引擎，以支持外部代码或使用 C 或 c + + 实现的外部运行时提供的 SQL Server 2016 中新的可扩展 API。 R 目前唯一支持的运行时。 BxlServer 来与通信使用 SQL 附属 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
 
  SQL 附属使用自定义数据格式进行了优化的快速数据传输之间 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和外部脚本语言。 它会执行类型转换并定义输入和输出数据集的架构之间的通信期间 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和。

  BxlServer 对这些任务使用 SQL 附属︰ 
  - 读取输入的数据
  - 写入输出数据
  - 获取输入的参数
  - 写入输出参数
  - 错误处理
  - 写入 STDOUT 和 STDERR 返回到客户端

  可以通过使用扩展事件监视 SQL 附属。 有关详细信息，请参阅 [扩展事件用于 SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)。


## 组件之间的信道

+ **TCP/IP** 默认情况下，之间的内部通信 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和 SQL 附属使用 TCP/IP。

+ **命名管道**

  BxlServer 之间的内部数据传输和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SQL 附属通过使用一种专有的压缩数据格式来提高性能。 通过命名管道 BXL 格式交换到 BxlServer R 内存中的数据。 
  
+ **ODBC** 外部数据科学客户端之间的通信和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例使用 ODBC。 发送 R 的帐户向作业 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 必须连接到的实例并运行外部脚本的这两个权限。 此外，该帐户必须有权访问作业，以写入数据 （例如，如果将结果保存到一个表），或创建数据库对象 （例如，如果将 R 函数另存为新的存储过程的一部分） 使用的任何数据。

  当 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 是 R 作业的计算上下文发送从远程客户端，以及 R 命令必须从外部源检索数据，ODBC 将使用写回。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将映射到当前实例上的用户的标识发出远程 R 命令的用户的标识，并运行在 ODBC 命令中用该用户的凭据。 用于执行此 ODBC 调用所需的连接字符串从客户端代码。
  
  可以通过使用脚本内发出其他 ODBC 调用 **RODBC**。 RODBC 是一个受欢迎的 R 包，用来访问关系数据库; 中的数据但是，其性能低于通常使用的提供程序可比较 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 许多 R 脚本中检索"辅助"数据集以供分析的一种方式使用嵌入的 RODBC 调用。 例如，训练模型的存储的过程可能会定义一个 SQL 查询来获取的数据用于定型模型，但使用嵌入的 RODBC 调用来获取其他因素，以执行查找，或从外部源，例如文本文件或 Excel 获得新的数据。

  下面的代码演示在 R 脚本中嵌入的 RODBC 调用︰
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **其他协议** 流程可能需要按"块"的工作或将数据传输回远程客户端还可以使用。所支持的 Microsoft R.实际数据传输的 XDF 格式是通过编码的 blob。

## 组件间的交互

刚才介绍了组件体系结构已提供了可保证"按原样"打开源 R 代码可协同工作，而极大地提供更高的性能上运行的代码 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机。 组件如何与 R 运行时交互的机制和 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 数据库引擎应用程序有所不同，具体取决于启动的 R 代码的方式。 在本部分总结了关键方案。 
 
### 从 SQL Server （数据库） 执行 R 脚本

从"内部"运行的 R 代码 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通过调用存储的过程执行。 因此，可以使存储的过程调用的任何应用程序可以启动 R 代码的执行。  此后 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 管理的 R 代码执行下面的关系图中进行了总结。

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. 由参数指示 R 运行时的请求 _@language = 'R'_ 传递给存储过程， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将此请求发送到快速启动板服务。
2. 在快速启动板服务启动相应的启动程序;在此情况下，RLauncher。
3. RLauncher 启动外部 R 进程。
4. BxlServer 协同 R 运行时，管理与数据交换 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和存储的工作结果。
5. 在整个，SQL 附属管理相关任务有关的通信，然后使用处理 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
6. BxlServer SQL 附属用于传达状态和结果传递给 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 获取结果并关闭相关的任务和流程。 


### 从远程客户端已执行的 R 脚本

当从支持 Microsoft R 的远程数据科学客户端连接，您可以运行 R 函数的上下文中 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用 ScaleR 函数。 这是与前一不同的工作流，下面的关系图中所述。


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. 对于 ScaleR 函数，R 运行时调用的链接的函数，后者又调用 BxlServer。 
2. BxlServer 提供与 Microsoft R，并从 R 运行时的单独进程中运行。
3. BxlServer 确定连接目标并启动使用 ODBC，传递过程中的 R 数据源对象的连接字符串中提供的凭据的连接。
4. BxlServer 打开的连接 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 实例。
5. 对于 R 调用，快速启动板服务调用，即启用启动适当的启动器 RLauncher。 此后，处理的 R 代码相当于从 T-SQL 中运行的 R 代码的过程。
6. RLauncher 对进行调用的实例上安装的 R 运行 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机。 
7. 结果将返回到 BxlServer。
8. SQL 附属管理与通信 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和清除相关的作业对象。
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将结果传递回客户端。

## 另请参阅
[体系结构概述](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
