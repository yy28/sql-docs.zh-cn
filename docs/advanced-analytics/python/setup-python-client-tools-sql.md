---
title: 设置与 SQL Server 一起使用的 Python 客户端工具 |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: c0054fd0dc9ecb3dbf9035ddff0f6828a85b471d
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="set-up-python-client-tools-for-use-with-sql-server"></a>设置 Python 与 SQL Server 一起使用的客户端工具 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何配置以支持在 SQL Server 中运行 Python 代码的 Windows 计算机上的 Python 环境。 这包括以下方案：

+ 测试和开发解决方案远程 Python 在工作站上，并将代码发送到 SQL Server，SQL Server 计算上下文中执行。 

    你通常想要安装的完备的 Python 开发环境。 
    
    本地 Python 环境应与 SQL Server 实例上的 Python 环境兼容，而且你必须安装支持远程计算上下文的库。

+ 开发和测试你的代码使用专用的 Python tools，然后将代码迁移到 SQL Server 以运行存储过程中。

    你将用于开发，关闭服务器的完备的 Python IDE。 但是，在部署你的代码之前，你将在模拟 SQL Server 环境的环境中测试它。

+ 主要在 SQL Server 中的存储过程运行 Python 代码，你不开发 Python 代码。 您希望代码已测试并调试之前将其包装在存储过程。 但是，有时你可能需要运行 SQL Server，以确定问题源外面的代码。

    你不希望在服务器上，安装任何 Python 工具，并且将使用与分发一起安装的默认工具。 你可能决定配置使用实例库，以验证代码适用之外的存储过程的 Python 环境。

## <a name="requirements"></a>需求

无论你使用用于开发 Python 代码的工具，当你在 SQL Server 中运行 Python 代码，或使用 SQL Server 数据时，将满足以下要求：

+ 若要使用 Python，SQL Server 2017 或更高版本是必需的。 你必须还安装的功能的支持机器学习服务 （数据库中），并显式启用该功能。 有关详细信息，请参阅[设置 SQL Server 2017](../r/set-up-sql-server-r-services-in-database.md)。

    如果你安装的 SQL Server 2017 早期版本，你可能会收到错误，如果你尝试运行此命令行实用工具从 Python 命令。 我们建议你[升级到最新版本](#bkmk_update)如有可能。 

+ 你必须确保运行的代码所使用的帐户具有连接到数据库并运行 Python 代码的权限。 特殊权限`EXECUTE ANY EXTERNAL SCRIPT`是必需的所有帐户的使用 R 或 Python 脚本。 

+ 你必须确保帐户具有要读取数据或创建新对象可能需要的任何数据库权限。 

+ 如果你的代码需要与 SQL Server 的默认情况下未安装的包，排列与数据库管理员能够实例所使用的 Python 环境中安装的包。 SQL Server 是一个受保护的环境，并且没有为安装包的限制。 

    不建议的包作为你的代码的一部分的即席安装，即使你具有权限。 此外，在 server 库中安装新包之前始终仔细考虑的安全隐患。

> [!NOTE]
> 如果你想要机器学习服务器上使用 Python，它支持其他计算上下文，如 Linux 或 Spark 群集，请参阅以下文章：
> 
> + [如何在 Windows 上本地安装自定义 Python 包和解释程序](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [将 Python 工具和 Ide 链接到与计算机学习服务器一起安装的 Python 解释程序](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>包括标准安装的默认工具

默认安装的 SQL Server 自 2017 年与机器学习服务 （数据库） 和 Python 添加了以下标准的 Python 工具和资源：

+ Python 示例数据
+ Anaconda 4.2 分发 
+ Python 可执行文件 python.exe 和 pythonw.exe

默认情况下，安装到此文件夹是： `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`。 

## <a name="open-python-from-the-command-line"></a>从命令行打开 Python 

若要使用 Python 运行时将随实例一起安装，可从安装路径中启动可执行 Python。 基本说明，子网上有[Python 为 Windows 常见问题](https://docs.python.org/3/faq/windows.html)。

> [!IMPORTANT]
> 通常情况下，若要避免资源争用，我们建议你**不这样做**Python 从实例库服务器上运行，如果您认为它是可能的 SQL Server 实例正在运行的 Python 代码。 但是，使用实例库中的工具可能会有价值，如果你尝试调试仅当在 SQL Server 中运行时，才会出现的问题并且想要查看更详细的错误消息，或请确保安装了所有所需的程序包。

1. 导航到安装实例库的文件夹。 例如，在默认安装中，文件夹是`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

2. 找到 Python.exe。 

3. 右键单击并选择**以管理员身份运行**以打开一个交互式命令行窗口。

## <a name="bkmk_update"></a> 更新 Python 组件

你可以更新 Python 组件通过下载并安装最新版本中，使用此处介绍的脚本： [Windows 上的安装 Python 客户端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> 下载脚本安装程序[SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)。 如果你需要不同版本，请参阅[安装没有 internet 访问权限的机器学习组件](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>设置 Python 开发环境

如果你只需正在调试从命令行脚本，可以通过使用标准与机器学习服务一起安装的 Python 工具来获取，或使用文本编辑器。 但是，如果你正在开发新的解决方案，或从远程客户端工作，我们建议使用为完备的 Python IDE。 常用的选项包括：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)与 Python
+ [AI 适用于 Visual Studio 的工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [在 Visual Studio 代码中的 Python](https://code.visualstudio.com/docs/languages/python)
+ 如 PyCharm、 Spyder 和 Eclipse 的常用第三方工具

我们建议 Visual Studio，因为它支持数据库项目，以及机器学习项目。 有关配置 Python 环境的帮助，请参阅[Visual Studio 中的管理 Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>安装 revoscalepy

即使你已成功安装机器学习服务，你可能会出现错误时尝试加载**revoscalepy**函数从 Python 命令行。 这些步骤介绍如何安装更新，从而允许使用**revoscalepy**。

1. 下载安装 shell 脚本从https://aka.ms/mls93-py(或使用https://aka.ms/mls-py9.2 有关。 发布的版本）。 脚本安装 Anaconda 4.2.0，其中包括 Python 3.5.2，以及前面列出的所有包。

2. （以管理员身份），使用提升的权限打开一个新的 PowerShell 窗口。

3. 打开在其中下载安装程序的文件夹并运行该脚本：

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

你还可以运行`-InstallFolder`命令行自变量并指定新路径作为命令的一部分。 例如： 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

如果遇到错误，你可能需要挂起执行策略为特定的文件，该会话的持续时间，如下所示： 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

此外可以在会话的持续时间内挂起执行策略。 使用此语句中，执行策略设置为`Unrestricted`会话的持续时间和不更改配置或将更改写入到磁盘。

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>验证 Python 和 revoscalepy 正常工作

在安装所有工具和库，你应连接到服务器并验证，你可以创建计算上下文，或 Python 能够与 SQL Server。

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>验证该 revoscalepy 从 Python 命令行中工作

若要验证**revoscalepy**可以加载模块，请在 Python 交互式命令提示符下运行下面的示例代码。 在代码中生成使用 Python 示例数据的数据摘要和[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)。 

```Python
import os
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

示例数据路径都将打印，以便你可以确定调用 Python 哪个实例。

### <a name="verify-that-python-can-be-called-from-sql-server"></a>验证，可以从 SQL Server 调用 Python

若要验证 Python 与 SQL Server 通信，请打开 SQL Server Management Studio。 (你可以使用另一个类似的工具，如[SQL 操作 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)。)打开一个新**查询**窗口并运行存储过程的上下文中的任何简单的 Python 命令：

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

可能需要一段时间才能启动 Python 运行时第一次，但如果没有错误，你知道正在 SQL Server 快速启动板，并可以从 SQL Server 启动 Python。

若要验证**revoscalepy**位于可用库中的 SQL Server 实例，运行该脚本基于[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)，与一些细微的修改来生成与 SQL Server 兼容的结果。 

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

因为 rx_summary 返回类型的对象`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多个元素，以处理 SQL Server 中的结果，你可以提取仅在以表格格式中的数据帧。

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>验证 Python 执行 SQL Server 中的远程计算上下文

如果你已安装**revoscalepy**在本地 Python 开发环境中，你应该能够连接到 SQL Server 2017 其中启用了 Python，一个实例，运行使用服务器作为计算类似的代码示例上下文。 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

在此示例中，返回到控制台中，而不被返回格式正确的表格数据到 SQL Server 的摘要的对象。 

此外，因为[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)已被调用，加载示例数据从 SQL Server 计算机上的示例文件夹而不是从本地示例文件夹。
