---
title: Python 编程语言扩展-SQL Server 机器学习
description: 了解有关 Python 代码执行和 SQL Server 2017 机器学习服务中内置的 Python 库。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: abf7028c8b55f4f97770586f2a678a538f01b29a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963044"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server 中的 Python 语言扩展
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 扩展是到关系数据库引擎的 SQL Server 机器学习服务外接程序的一部分。 添加 Python 执行环境，使用 Python 3.5 运行时和解释器，标准库和工具以及 Microsoft 产品库适用于 Python 的 Anaconda 分发版： [revoscalepy](../python/ref-py-revoscalepy.md)用于分析在规模和[microsoftml](../python/ref-py-microsoftml.md)完成机器学习算法。 

作为安装 Python 集成[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)。

安装 Python 3.5 运行时和解释器可确保与标准 Python 解决方案几近完整兼容性。 从 SQL Server，以确保不受到影响数据库操作中的单独进程中运行 Python。

## <a name="python-components"></a>Python 组件

SQL Server 包含的开源和专有的包。 安装程序安装的 Python 运行时是 Anaconda 4.2 使用 Python 3.5。 Python 运行时安装独立于 SQL 工具和可扩展性框架中的核心引擎进程之外执行。 作为与 Python 配合使用的机器学习服务安装的一部分，您必须同意 GNU 公共许可证的条款。 

SQL Server 不会修改 Python 可执行文件，但必须使用安装由安装程序，因为在该版本是专有的包，生成并测试上的 Python 版本。 Anaconda 分发版支持包的列表，请参阅 Continuum analytics 站点：[Anaconda 包列表](https://docs.continuum.io/anaconda/packages/pkg-docs)。

可以与实例关联的文件夹中找到与特定的数据库引擎实例相关联的 Anaconda 分发版。 如果默认实例上，可以使用机器学习服务和 Python 安装 SQL Server 2017 数据库引擎，例如下, 查找`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

Microsoft 通过添加并行和分布式工作负荷的 Python 包包括以下库。

| 库 | 描述 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 支持数据源对象和数据探索、 操作、 转换和可视化效果。 它支持远程计算上下文，以及各种可缩放的机器学习模型的创建，如**rxLinMod**。 有关详细信息，请参阅[revoscalepy 模块与 SQL Server](../python/ref-py-revoscalepy.md)。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 包含机器学习算法，经过优化的速度和准确性，以及行中使用文本和图像的转换。 有关详细信息，请参阅[microsoftml 模块与 SQL Server](../python/ref-py-microsoftml.md)。 |

紧密耦合 Microsoftml 并 revoscalepy;microsoftml 中使用数据源定义为 revoscalepy 对象中。 计算上下文到 microsoftml revoscalepy 传输中的限制。 也就是说，所有功能都都可用于本地操作，但切换到远程计算上下文需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>在 SQL Server 中使用 Python

导入**revoscalepy**模块转换在 Python 代码，然后调用函数的模块，与任何其他 Python 函数类似。

支持的数据源包含 ODBC 数据库、 SQL Server 和 XDF 文件格式来交换数据使用其他源，或使用 R 解决方案。 用于 Python 的输入的数据必须是表格。 中的窗体必须返回所有 Python 结果**pandas**数据帧。

支持的计算上下文包括本地或远程 SQL Server 计算上下文。 远程计算上下文是指在工作站上，例如一台计算机启动的执行代码但开关，则脚本执行过程转移到远程计算机。 切换计算上下文需要两个系统都在同一 revoscalepy 库。

本地计算上下文中，正如您所料，包括执行的 T-SQL 代码与作为数据库引擎实例在同一服务器上的 Python 代码，或嵌入在存储过程。 此外可以从本地 Python IDE 运行代码并让脚本在 SQL Server 计算机上执行，通过定义远程计算上下文。

## <a name="execution-architecture"></a>执行体系结构

下图展示了与每个支持的方案中的 Python 运行时交互的 SQL Server 组件： 从 Python 终端，使用 SQL Server 计算上下文中运行脚本，数据库和远程执行。

### <a name="python-scripts-executed-in-database"></a>在数据库中执行 Python 脚本

"内部"SQL Server 的 Python 运行时，必须将封装在特殊的存储过程，Python 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

已在存储过程中嵌入脚本后，可以使存储的过程调用的任何应用程序可以启动 Python 代码的执行。  此后，SQL Server 管理代码执行下面的关系图中进行了总结。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. 参数指示的 Python 运行时的请求`@language='Python'`传递给存储过程。 SQL Server 将此请求发送到快速启动板服务。
2. 快速启动板服务启动相应的启动器;在此情况下，PythonLauncher。
3. PythonLauncher 启动外部 Python35 进程。
4. BxlServer 协调与 Python 运行时，若要管理的数据交换和存储工作结果。
5. SQL Satellite 管理有关相关的任务和进程与 SQL Server 的通信。
6. BxlServer 使用 SQL Satellite 状态以及到 SQL Server 的结果进行通信。
7. SQL Server 获取结果并关闭相关的任务和流程。

### <a name="python-scripts-executed-from-a-remote-client"></a>从远程客户端执行 Python 脚本

您可以从远程计算机，如便携式计算机，运行 Python 脚本并将它们在 SQl Server 计算机的上下文中执行，如果满足这些条件：

+ 相应地设计脚本
+ 远程计算机安装了由机器学习服务的可扩展性库。 [Revoscalepy](../python/ref-py-revoscalepy.md)包所需使用远程计算上下文。

下图总结了整个工作流，脚本会从远程计算机时。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 中支持的函数**revoscalepy**，Python 运行时将调用一个链接函数，接着调用 BxlServer。
2. BxlServer 附带机器学习服务 （数据库内），并从 Python 运行时的单独进程中运行。
3. BxlServer 确定连接目标并启动使用 ODBC，传递作为 Python 脚本中的连接字符串的一部分提供的凭据的连接。
4. BxlServer 打开到 SQL Server 实例的连接。
5. 当调用的外部脚本运行时，调用该快速启动板服务，这进而会启动相应的启动器： 在此情况下，PythonLauncher.dll。 此后，处理 Python 代码处理类似于工作流中时从 T-SQL 中的存储过程调用 Python 代码。
6. PythonLauncher 调用的实例的 SQL Server 计算机安装 Python。
7. 将结果返回到 BxlServer。
8. SQL Satellite 管理与 SQL Server 和相关的作业对象清理的通信。
9. SQL Server 会将结果传递回客户端。

## <a name="see-also"></a>请参阅

+ [SQL Server 中的 revoscalepy 模块](../python/ref-py-revoscalepy.md)
+ [revoscalepy 函数参考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server 中的可扩展性框架](extensibility-framework.md)
+ [R 和机器学习中 SQL Server 的扩展](extension-r.md)