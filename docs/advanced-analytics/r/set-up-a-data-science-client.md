---
title: 设置 SQL Server 上的 R 开发数据科学客户端 |Microsoft Docs
description: 远程连接到 SQL Server 的开发工作站上安装本地 R 库和工具。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a88269ff6b55aa473c48cfa0937e926770bbaff1
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462103"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>设置 SQL Server 上的 R 开发数据科学客户端
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

配置的实例后[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]若要支持机器学习，应设置 R 开发环境能够连接到用于远程执行和部署服务器。

### <a name="evaluation-and-independent-development"></a>评估和独立开发
 
如果你有开发人员版和计划在本地处理 R 脚本计划移到 SQL Server，可以跳到[安装 IDE](#install-ide)并将该工具指向本地 SQL Server 使用的 R 库。

> [!Tip]
> 演示和视频演练，请参阅[运行 R 和远程 SQL Server 从 Jupyter Notebook 或任何 IDE 中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)或这[YouTube 视频](https://youtu.be/D5erljpJDjE)。

## <a name="1---install-r-packages"></a>1-安装 R 包

Microsoft 产品中的 R 功能是多层。 它启动与 Microsoft 的开放源代码基础 R 发行版，但然后扩展使用特定于产品的包时，如[RevoScaleR](revoscaler-overview.md)，，启用远程计算上下文和 R 任务的并行执行。

客户端和远程服务器之间的协调的操作需要这两个具有相同的包的系统。 若要获取的客户端工作站上的库的完整补集，安装下表中一个软件程序包。 

| 库提供程序 | 用法  |
|------------------|--------------------------------|
| [Microsoft R Client](http://aka.ms/rclient/download) |  此免费下载提供 RevoScaleR、 MicrosoftML 和其他 R 包，但其上限为两个线程和内存中的数据。 但是，可以仍创建本地启动的 R 解决方案，并迁移执行 (称为*计算上下文*) 访问数据和远程 SQL Server 实例的计算能力。 这是客户端集成与生产 SQL Server 实例的推荐的方法。 有关此工具的详细信息，请参阅[什么是 Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)。|
| 独立服务器 | 下**共享功能**，SQL Server 安装程序包含可用于 SQL Server 2016 R Services 和 SQL Server 2017 机器学习的独立服务器安装选项。 这些是全功能的服务器，能够连接到和使用多个数据平台中的数据完全从 SQL Server 中分离。 但你可能无法使用客户端容量中软件访问 SQL Server 数据库引擎实例正在运行的 R 和 Python 的任务。 [SQL Server 2017 机器学习服务器 （独立）](../install/sql-machine-learning-standalone-windows-install.md)已作为 SQL Server 2017 机器学习实例相同的库。 [SQL Server 2016 R Server （独立版）](../install/sql-r-standalone-windows-install.md)具有与 SQL Server 2016 R Services 的同一个库。 |


<a name="r-tool"></a>
 
## <a name="2---open-an-r-prompt"></a>2-打开 R 提示符

使用 SQL Server 安装 R，可以获取相同的 R 工具的标准到 R，例如 RGui 和 Rterm，等任何基本安装。 这些工具是轻量，可用于检查包和库的信息、 运行临时命令或脚本，或逐步执行教程。 这些工具可用于获取 R 版本信息，并确认连接。

若要使用 R 与 SQL Server 或 R 客户端一起安装的版本，请从 SQL Server 或 R 客户端程序文件夹中打开 R 提示符。 以下步骤适用于 R 客户端和 RGui.exe。

1. 对于 R 客户端，请转到`~\Program Files\Microsoft\R Client\R_SERVER\bin\x64`。
2. 双击**RGui.exe**若要使用 R 命令提示符启动 R 会话。

从 Microsoft 程序文件夹中，多个包，包括 RevoScaleR，启动 R 会话时自动加载。 输入**search （)** 在 R 提示符处进行确认。

   ![版本信息时加载 R](../install/media/rclient-rgui-r-prompt.png "打开 R 提示符")

### <a name="tool-list-and-location"></a>工具列表和位置

| 工具 | Description | 
|------|-------------|
| **RTerm**: | 命令行终端中运行 R 脚本 | 
| **RGui.exe** | 一个简单的交互式编辑器为。 的命令行自变量是 RGui.exe 和 RTerm 相同的。 |
| **RScript** | 用于在批处理模式下运行 R 脚本的命令行工具。 |

工具位于**bin**文件夹安装的 SQL Server 作为基本 R 或 R 客户端。 以下路径有效的工具，具体取决于哪些产品版本和功能安装位置：

| Microsoft 产品 | R 工具位置 |
|-------------------|-----------------|
| Microsoft R Client | `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64` |
| Microsoft 机器 Learning (R) 服务器 | `~\Program Files\Microsoft\R_SERVER\bin\x64`
| SQL Server 2016 R 服务 | `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2016 R 独立服务器 | `~\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64` 
| SQL Server 2017 机器学习 (R) 服务 | `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2017 机器学习 (R) 独立服务器 | `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` |

## <a name="3---permissions"></a>3-权限

若要连接到要运行脚本和上传数据的 SQL Server 实例，必须在数据库服务器上具有有效的登录名。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议使用 Windows 集成身份验证，但使用 SQL 登录名是在某些情况下更简单。

最小值，用来运行代码的帐户必须具有你正在使用，加上特殊权限执行任意外部脚本从数据库中读取的权限。 大多数开发人员还需要在存储过程包含在脚本中，窗体中创建新对象的权限和将数据写入到包含训练数据的表或评分的数据。 

请求数据库管理员，使用： 在数据库中配置以下权限的帐户

+ **EXECUTE ANY EXTERNAL SCRIPT**在服务器上运行 R。
+ **db_datareader**权限才能运行用于定型模型的查询。
+ **db_datawriter**编写定型数据或评分的数据。
+ **db_owner**以创建对象的存储过程，如表、 函数。 
  您还需要**db_owner**创建示例，并测试数据库。 

如果你的代码需要与 SQL Server 的默认情况下不安装的程序包，排列与数据库管理员能够与实例安装的包。 SQL Server 是一个受保护的环境并在其中安装包的限制。 不建议临时安装的包作为你的代码的一部分，即使您具有权限。 此外，server 库中安装新包之前始终仔细考虑的安全隐患。

> [!Tip]
> 如果您不熟悉 SQL Server 和本地开发环境中的工作，您可以逐步完成本教程，若要了解有关登录名和设置权限：[到 RevoScaleR 深入研究](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

## <a name="4---test-connections"></a>4-测试连接

必须启用 SQL Server[远程连接](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)并且必须具有的权限，包括用户登录名和要连接到数据库。 下面的步骤假定演示数据库[NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)和 Windows 身份验证。

 作为验证步骤，使用内置工具和 RevoScaleR 以确认连接到远程服务器。

1. 首先[打开 R 工具](#r-tool)客户端工作站上。 RevoScaleR 会自动加载。 例如，请转到`~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`，然后双击**RGui.exe**来启动它。

2. 确认 RevoScaleR 可以正常运行的通过运行以下命令，返回一个演示数据集的统计摘要。 请确保提供 SQL Server 数据库引擎实例的有效的服务器名称。

```r
connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
testQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
cc <-RxInSqlServer(connectionString=connStr)
rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=testQuery, connectionString=connStr), computeContext=cc)
```
此脚本连接到远程服务器上的数据库，提供查询、 创建计算上下文`cc`指令的远程执行代码，然后提供的 RevoScaleR 函数**rxSummary**返回统计查询结果的摘要。

<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-安装 IDE

对于持续和严重开发项目，则应安装集成的开发环境 (IDE)。 SQL Server 工具和内置的 R 工具未配备繁重的 R 开发中。 工作代码后，可以将其部署为 SQL Server 上执行的存储过程。

您应指向本地 R 库的 IDE： 基本 R、 RevoScaleR，等等。 远程 SQL 服务器上运行的工作负荷执行脚本期间发生，当您的脚本调用访问数据和操作该服务器上的 SQL 服务器上的远程计算上下文。

### <a name="rstudio"></a>RStudio

使用时[RStudio](https://www.rstudio.com/)，可以配置要使用的 R 库和对应于远程 SQL 服务器上的可执行文件的环境。

1. 检查 SQL Server 上安装 R 包版本。 有关详细信息，请参阅[获取 R 包信息](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。

1. 安装 Microsoft R 客户端或独立服务器选项，以添加 RevoScaleR 和其他 R 包，包括 SQL Server 实例使用的基础 R 发行版之一。 选择在同一版本级别或更低 （包是向后兼容），它提供与服务器上的相同包版本。 有关版本信息，请参阅这篇文章中映射的版本：[升级 R 和 Python 组件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

1. 在 RStudio 中，[更新 R 路径](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)以指向提供 RevoScaleR、 Microsoft R Open，以及其他 Microsoft 包的 R 环境。 根据如何获取 RevoScaleR 和其他库，它是最有可能的以下路径：

  + C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library
  + C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library
  + C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64

### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools for Visual Studio (RTVS)

如果你还没有首选的 IDE 适用于 R，我们建议**针对 Visual Studio 的 R 工具**。

+ [下载 R Tools for Visual Studio (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [安装说明](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio)-RTVS 是在多个 Visual Studio 版本中可用。
+ [入门 Visual Studio 的 R 工具](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>从 RTVS 连接到 SQL Server

此示例使用 Visual Studio 2017 Community Edition 已安装数据科学工作负载。

1. 从**文件**菜单中，选择**新建**，然后选择**项目**。

2. 在左侧窗格列出了预安装的模板。 单击**R**，然后选择**R 项目**。 在中**名称**框中，键入`dbtest`然后单击**确定**。 

  Visual Studio 将创建一个新的项目文件夹和默认脚本文件， `Script.R`。 

3. 类型`.libPaths()`脚本的第一行上文件，，然后按 CTRL + ENTER。

  当前的 R 库路径应显示在**R 交互**窗口。 

4. 单击**的 R 工具**菜单，然后选择**Windows**若要查看其他特定于 R 的窗口都可以在你的工作区中显示的列表。
 
    + 通过按 CTRL + 3 查看当前存储库中的包上的帮助。
    + 请参阅中的 R 变量**变量资源管理器**，通过按 CTRL + 8。

5. 创建 SQL Server 实例的连接字符串和 RxInSqlServer 构造函数中使用的连接字符串创建 SQL Server 数据源对象。 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```
    > [!TIP]
    > 若要运行批处理，选择你想要运行并按 CTRL + ENTER 行中。

6. 将计算上下文设置为该服务器，并对数据运行一些简单的 R 代码。

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    在返回结果**R 交互**窗口。
    
    如果你想要确保 SQL Server 实例上执行的代码，可以使用 Profiler 创建跟踪。

## <a name="next-steps"></a>后续步骤

两个不同教程包括练习，以便您可以练习切换到远程 SQL Server 实例从本地计算上下文。

+ [教程： 使用 RevoScaleR R 函数与 SQL Server 数据](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)