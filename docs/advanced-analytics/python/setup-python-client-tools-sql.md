---
title: 设置为用于 SQL Server 机器学习 Python 客户端工具 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f6823870060992586756dffa93aac6937d27d65
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "40401297"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>设置 Python 与 SQL Server 机器学习一起使用的客户端工具
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

从 SQL Server 2017 或更高版本，开始时添加到机器学习服务 （数据库内） 的 Python 支持提供 Python 集成。 有关详细信息，请参阅[安装 SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。

在本文中，了解如何配置开发工作站，以便可以连接到远程 SQL Server 启用了 Python。

### <a name="evaluation-and-independent-development"></a>评估和独立开发
 
如果你有开发人员版和计划 Python 脚本在本地处理你计划将移动到 SQL Server，可以跳到[安装 IDE](#install-ide)并将该工具指向本地 SQL Server 使用的 Python 库。

> [!Tip]
> 演示和视频演练，请参阅[运行 R 和远程 SQL Server 从 Jupyter Notebook 或任何 IDE 中的 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)或这[YouTube 视频](https://youtu.be/D5erljpJDjE)。

## <a name="1---install-python-packages"></a>1-安装 Python 包

本地工作站必须具有与 SQL Server 上的相同 Python 包版本： revoscalepy 和 microsftml。 其他 Python 包可用，但更常用于与在独立 （非实例） 的机器学习服务器上下文中的其他方案。 

1. 下载中的安装 shell 脚本[ https://aka.ms/mls93-py ](https://aka.ms/mls93-py) (或使用[ https://aka.ms/mls-py ](https://aka.ms/mls-py) 9.2 的。 发行版）。 该脚本安装 Anaconda 4.2.0，其中包括 Python 3.5.2，以及前面列出的所有包。

  通过提供了 Python 组件[SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)。 如果需要不同版本，请参阅[CAB 下载](../install/sql-ml-cab-downloads.md)

2. 使用提升的管理员权限打开 PowerShell 窗口 (右键单击**以管理员身份运行**)。

3. 转到下载安装程序的文件夹并运行该脚本。 添加`-InstallFolder`命令行参数来指定库的文件夹位置。 例如： 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls")
   ```

   安装需要一些时间才能完成。 你可以监视在 PowerShell 窗口中的进度。 安装程序完成后，你有一组完整的包。 例如，如果您指定`C:\mspythonlibs`作为文件夹的名称，您会发现在包`C:\mspythonlibs\Lib\site-packages`。 否则，默认文件夹是`C:\Program Files\Microsoft\PyForMLS1`。

安装脚本不会修改您的计算机上的 PATH 环境变量，因此新的 python 解释器和您刚刚安装的模块不是自动提供给您的工具。 将 Python 解释器和库链接到工具的帮助，请参阅[5-安装 IDE](#install-ide)。

<a name="python-tool"></a>
 
## <a name="2---open-a-python-prompt"></a>2-打开 Python 提示符

Microsoft 中的 Python 集成包括内置的工具和数据以外的 microsoftml revoscalepy 等的特定于产品的库。 安装程序完成时，以下各项的客户端和服务器实例上的可用：

+ Python 示例数据
+ Anaconda 4.2 分发版 
+ Python 可执行文件 python.exe 和 pythonw.exe

> [!Tip] 
> 我们建议[Python 为 Windows 常见问题](https://docs.python.org/3/faq/windows.html)有关在 Windows 上运行 Python 程序的常规 purppose 信息。

### <a name="on-client-workstations"></a>客户端工作站上

若要使用安装脚本安装 Python 可执行文件：

1. 转到`C:\Program Files\Microsoft\PyForMLS\python.exe`或安装路径为选择任何位置。

2. 右键单击**Python.exe** ，然后选择**以管理员身份运行**打开交互式命令行窗口。

### <a name="on-sql-server"></a>SQL Server 上

SQL Server 安装程序将标准的 Python 工具和资源添加到服务器实例。 如果您使用的开发人员版，并且想要检查的 Python 版本或运行临时命令：

1. 转到`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

2. 右键单击**Python.exe** ，然后选择**以管理员身份运行**打开交互式命令行窗口。

> [!Note]
> 通常情况下，若要避免资源争用，我们建议您**不这样做**Python 从库中运行实例的服务器上，如果您认为不可能的 SQL Server 实例正在运行的 Python 代码。 但是，使用实例库中的工具可能很有价值，如果想要调试 SQL Server 中运行时，会发生的问题，并且想要查看更详细的错误消息，或请确保安装了所有所需的包。

## <a name="3---permissions"></a>3-权限

若要连接到要运行脚本和上传数据的 SQL Server 实例，必须在数据库服务器上具有有效的登录名。 可以使用 SQL 登录凭据或集成 Windows 身份验证信息。 我们通常建议使用 Windows 集成身份验证，但使用 SQL 登录名是在某些情况下更简单。

最小值，用来运行代码的帐户必须具有你正在使用，加上特殊权限执行任意外部脚本从数据库中读取的权限。 大多数开发人员还需要在存储过程包含在脚本中，窗体中创建新对象的权限和将数据写入到包含训练数据的表或评分的数据。 

询问数据库管理员可以在其中使用 Python 在数据库中配置的帐户的以下权限：

+ **EXECUTE ANY EXTERNAL SCRIPT**若要在服务器上运行 Python。
+ **db_datareader**权限才能运行用于定型模型的查询。
+ **db_datawriter**编写定型数据或评分的数据。
+ **db_owner**以创建对象的存储过程，如表、 函数。 
  您还需要**db_owner**创建示例，并测试数据库。 

如果你的代码需要与 SQL Server 的默认情况下不安装的程序包，排列与数据库管理员能够与实例安装的包。 SQL Server 是一个受保护的环境并在其中安装包的限制。 不建议临时安装的包作为你的代码的一部分，即使您具有权限。 此外，server 库中安装新包之前始终仔细考虑的安全隐患。

## <a name="4---test-connections"></a>4-测试连接

在安装所有工具和库，您应连接到服务器并验证您可以创建计算上下文，或 Python 可与 SQL Server 通信。

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>验证该 revoscalepy Python 命令行中正常工作

若要确认**revoscalepy**可以加载模块，请从 Python 交互式命令提示符下运行下面的示例代码。 在代码中生成数据摘要，使用 Python 示例数据并[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)。 

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

示例数据路径被打印，以便你可以确定正在调用 Python 哪个实例。

### <a name="verify-that-python-can-be-called-from-a-local-sql-server"></a>确认可以从本地 SQL Server 调用 Python

在本地开发环境中，验证是否在与本地通信 Python[配置为外部脚本的 SQL Server 实例](../install/sql-machine-learning-services-windows-install.md)。 使用 SQL Server Management Studio 打开一个新**查询**窗口并运行存储过程的上下文中的任何简单的 Python 命令：

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

可能需要一段时间才能启动 Python 运行时的第一次，但如果没有任何错误，您知道使用 SQL Server 快速启动板，并且可以从 SQL Server 启动 Python。

若要确认**revoscalepy**目前在运行基于脚本的 SQL Server 实例库[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)，进行一些细微的修改，以生成与 SQL Server 兼容的结果。 

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

因为 rx_summary 返回类型的对象`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多个元素，可以处理 SQL Server 中的结果，可以提取只是一个表格中的数据帧。

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>验证 SQL Server 中的 Python 执行作为远程计算上下文

如果已安装**revoscalepy**应在本地 Python 开发环境中，将无法连接到在其中启用了 Python，SQL Server 2017 的远程实例并运行一个类似的代码示例使用作为服务器计算上下文。 

若要运行此脚本，指定有效的服务器名称和现有的数据库。 此特定脚本不会使用数据库，但连接字符串需要它。

```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=<server-name>;Database=TestDB;Trusted_Connection=True"
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

在此示例中，返回到控制台中，而不是到 SQL Server 返回格式正确的表格数据的摘要的对象。 

此外，由于[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)已被调用，加载示例数据从 SQL Server 计算机上的 samples 文件夹，而不是从您的本地 samples 文件夹。


<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-安装 IDE

如果只要调试脚本从命令行，您可以通过获取的标准的 Python 工具。 但是，如果要开发新的解决方案，或从远程客户端工作，我们建议使用全面的 Python IDE。 常用选项包括：

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/)与 Python 配合使用
+ [用于 Visual Studio 的 AI 工具](https://docs.microsoft.com/visualstudio/ai/installation)
+ [在 Visual Studio Code 中的 Python](https://code.visualstudio.com/docs/languages/python)
+ 常用的第三方工具如 PyCharm、 Spyder 和 Eclipse

我们建议 Visual Studio，因为它支持数据库项目，以及机器学习项目。 为了帮助您配置的 Python 环境，请参阅[Visual Studio 中的管理 Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)。

因为开发人员经常使用多个版本的 Python，安装程序不向路径添加 Python。 若要使用的 Python 可执行文件和由安装程序安装的库，链接到你的 IDE **Python.exe**还提供了 revoscalepy 和 microsoftml 的路径处。 例如，为 Visual Studio 中的 Python 项目，自定义环境将指定`C:\Program Files\Microsoft\PyForMLS`，`C:\Program Files\Microsoft\PyForMLS\python.exe`并`C:\Program Files\Microsoft\PyForMLS\pythonw.exe`有关**前缀路径**，**解释器路径**，和**窗口化解释器**分别。

有关其他指南，请参阅[链接 Python 工具和 Ide](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。 本文面向 Microsoft 机器学习服务器以便 Python 路径不同，但它演示如何使用各种工具链接到 Python 库。

## <a name="next-steps"></a>后续步骤

现在，有工具和有效的连接到 SQL Server 的分步教程，以获取进一步了解 revoscalepy 函数和切换计算上下文。

> [!div class="nextstepaction"]
> [使用 revoscalepy 和远程计算上下文创建模型](../tutorials/use-python-revoscalepy-to-create-model.md)