---
title: Python 编程语言扩展
description: 了解 SQL Server 机器学习服务中的 Python 代码执行和内置 Python 库。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 61a1a5629d4f0488b5f75a08578c39f2e68f2c7d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715872"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server 中的 Python 语言扩展
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 扩展是关系数据库引擎的 SQL Server 机器学习服务外接程序的一部分。 它添加了一个 Python 执行环境、Anaconda 分发和 Python 3.5 运行时和解释器、标准库和工具, 以及适用于 Python 的 Microsoft 产品库: 用于进行大规模分析的[revoscalepy](../python/ref-py-revoscalepy.md)和[microsoftml](../python/ref-py-microsoftml.md)机器学习算法。 

Python 集成作为[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)安装。

安装 Python 3.5 运行时和解释器可确保与标准 Python 解决方案近乎完全兼容。 Python 在与 SQL Server 不同的进程中运行, 以确保不会危及数据库操作的安全。

## <a name="python-components"></a>Python 组件

SQL Server 包括开源和专用包。 安装程序安装的 Python 运行时是使用 Python 3.5 的 Anaconda 4.2。 Python 运行时独立于 SQL 工具进行安装, 并在扩展框架的核心引擎进程之外执行。 作为机器学习服务与 Python 一起安装的一部分, 你必须同意 GNU 公共许可证的条款。 

SQL Server 不会修改 Python 可执行文件, 但必须使用安装程序安装的 Python 版本, 因为该版本是专用包的生成和测试版本。 有关 Anaconda 分布支持的程序包列表, 请参阅 Continuum analytics 网站:[Anaconda 包列表](https://docs.continuum.io/anaconda/packages/pkg-docs)。

与特定数据库引擎实例关联的 Anaconda 分发可在与该实例关联的文件夹中找到。 例如, 如果在默认实例上安装了包含机器学习服务和 Python SQL Server 2017 数据库引擎, 请参阅`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

Microsoft 为并行和分布式工作负荷添加的 Python 包包含以下库。

| 库 | 描述 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 支持数据源对象和数据浏览、操作、转换和可视化。 它支持创建远程计算上下文, 以及各种可缩放的机器学习模型, 如**rxLinMod**。 有关详细信息, 请参阅[revoscalepy 模块与 SQL Server](../python/ref-py-revoscalepy.md)。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 包含经过优化以实现速度和准确性的机器学习算法, 以及用于处理文本和图像的行内转换。 有关详细信息, 请参阅[microsoftml 模块与 SQL Server](../python/ref-py-microsoftml.md)。 |

Microsoftml 和 revoscalepy 紧密耦合;microsoftml 中使用的数据源定义为 revoscalepy 对象。 Revoscalepy 传输到 microsoftml 时的计算上下文限制。 也就是说, 所有功能都可用于本地操作, 但切换到远程计算上下文需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>在 SQL Server 中使用 Python

将**revoscalepy**模块导入到 Python 代码, 然后从模块调用函数, 就像其他任何 Python 函数一样。

支持的数据源包括 ODBC 数据库、SQL Server 和 XDF 文件格式, 以便与其他源或通过 R 解决方案交换数据。 Python 的输入数据必须为表格格式。 所有 Python 结果必须以**pandas**数据帧的形式返回。

支持的计算上下文包括本地或远程 SQL Server 计算上下文。 远程计算上下文指的是在一台计算机 (如工作站) 上启动的代码执行, 但随后会将脚本执行切换到远程计算机。 切换计算上下文要求两个系统都具有相同的 revoscalepy 库。

如您所料, 本地计算上下文包括: 在与数据库引擎实例相同的服务器上执行 Python 代码, 并在 T-sql 中或在存储过程中嵌入代码。 还可以通过定义远程计算上下文, 从本地 Python IDE 运行代码, 并在 SQL Server 计算机上执行脚本。

## <a name="execution-architecture"></a>执行体系结构

以下关系图说明了在每个支持的方案中 SQL Server 组件与 Python 运行时的交互: 通过使用 SQL Server 计算上下文从 Python 终端运行脚本和远程执行。

### <a name="python-scripts-executed-in-database"></a>已在数据库中执行 Python 脚本

在 SQL Server 中运行 Python 时, 必须将 Python 脚本封装在一个特殊的存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中。

在将脚本嵌入到存储过程中后, 任何可进行存储过程调用的应用程序都可以启动 Python 代码的执行。  之后 SQL Server 按下图所概括的方式管理代码执行。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 运行时的请求通过传递给存储过程的`@language='Python'`参数来指示。 SQL Server 将此请求发送到快速启动板服务。
2. 启动板服务会启动相应的启动程序;在本例中为 PythonLauncher。
3. PythonLauncher 启动外部 Python35 进程。
4. BxlServer 协调使用 Python 运行时来管理数据的交换和工作结果的存储。
5. SQL 附属项管理有关与 SQL Server 相关的任务和进程的通信。
6. BxlServer 使用 SQL 附属项将状态和结果传递到 SQL Server。
7. SQL Server 获取结果并关闭相关任务和进程。

### <a name="python-scripts-executed-from-a-remote-client"></a>从远程客户端执行的 Python 脚本

如果满足以下条件, 则可以从远程计算机 (如便携式计算机) 运行 Python 脚本, 并在 SQl Server 计算机的上下文中执行这些脚本:

+ 适当地设计脚本
+ 远程计算机已安装机器学习服务使用的扩展性库。 使用远程计算上下文需要[revoscalepy](../python/ref-py-revoscalepy.md)包。

下图汇总了从远程计算机发送脚本时的总体工作流。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 对于在**revoscalepy**中支持的函数, Python 运行时将调用一个链接函数, 该函数反过来调用 BxlServer。
2. BxlServer 包含在机器学习服务 (数据库内), 并在独立于 Python 运行时的进程中运行。
3. BxlServer 确定连接目标, 并使用 ODBC 发起连接, 传递在 Python 脚本中作为连接字符串的一部分提供的凭据。
4. BxlServer 将打开与 SQL Server 实例的连接。
5. 调用外部脚本运行时, 将调用快速启动板服务, 后者会启动相应的启动程序: 在本例中为 PythonLauncher。 此后, 当从 T-sql 中的存储过程调用 Python 代码时, 将在工作流中处理 Python 代码处理。
6. PythonLauncher 对安装在 SQL Server 计算机上的 Python 实例进行调用。
7. 将结果返回到 BxlServer。
8. SQL 附属项管理与相关作业对象 SQL Server 和清理的通信。
9. SQL Server 将结果传递回客户端。

## <a name="see-also"></a>请参阅

+ [SQL Server 中的 revoscalepy 模块](../python/ref-py-revoscalepy.md)
+ [revoscalepy 函数引用](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server 中的扩展性框架](extensibility-framework.md)
+ [SQL Server 中的 R 和机器学习扩展](extension-r.md)