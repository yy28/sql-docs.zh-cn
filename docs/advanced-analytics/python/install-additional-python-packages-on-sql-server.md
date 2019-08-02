---
title: 安装新的 Python 语言包
description: 将新的 Python 包添加到 SQL Server 机器学习服务 (数据库内) 和 Machine Learning Server (独立)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e107622655d5f00d27de6abcea46a92526f47ada
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715806"
---
# <a name="install-new-python-packages-on-sql-server"></a>在 SQL Server 上安装新的 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何在 SQL Server 机器学习服务的实例上安装新的 Python 包。 通常, 安装新包的过程与标准 Python 环境中的过程类似。 但是, 如果服务器没有 internet 连接, 则需要执行一些其他步骤。

有关包位置和安装路径的详细信息, 请参阅[获取 R 或 Python 包信息](../package-management/installed-package-information.md)。

## <a name="prerequisites"></a>先决条件

+ 通过 Python language 选项[SQL Server 机器学习服务 (数据库内)](../install/sql-machine-learning-services-windows-install.md) 。 

+ 包必须符合 Python 3.5 标准并在 Windows 上运行。 

+ 安装包需要对服务器的管理访问权限。

## <a name="considerations"></a>注意事项

添加包之前, 请考虑包是否适合 SQL Server 环境。 通常, 数据库服务器是容纳多个工作负荷的共享资产。 如果添加的包在服务器上施加了太多的计算压力, 性能将会降低。 

此外, 某些常用的 Python 包 (如 Flask) 执行的任务更适合独立环境。 建议你使用 Python 数据库中的任务, 这些任务受益于与数据库引擎 (如机器学习) 的紧密集成, 而不是只查询数据库的任务。

数据库服务器经常被锁定。 在许多情况下, 完全阻止 Internet 访问。 对于具有很长依赖项的包, 需要提前标识这些依赖项, 并愿意手动安装每个依赖项。

## <a name="add-a-new-python-package"></a>添加新的 Python 包

在此示例中, 我们假设你想要在 SQL Server 计算机上直接安装新的包。

包安装按实例进行。 如果有多个机器学习服务实例, 则必须将包添加到每个实例中。

此示例中安装的包是[CNTK](https://docs.microsoft.com/cognitive-toolkit/), 它是 Microsoft 提供的一种深入学习的框架, 支持自定义、培训和共享不同类型的神经网络。

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步骤 1. 下载 Python 包的 Windows 版本

+ 如果要在无法访问 internet 的服务器上安装 Python 包, 则必须将 WHL 文件下载到另一台计算机, 然后将其复制到服务器。

    例如, 你可以在单独的计算机上从此站点[https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)下载 WHL 文件, 然后将该文件`cntk-2.1-cp35-cp35m-win_amd64.whl` 复制到 SQL Server 计算机上的本地文件夹。

+ SQL Server 2017 使用 Python 3.5。 

> [!IMPORTANT]
> 确保获取包的 Windows 版本。 如果文件以 gz 结束, 则它可能不是正确的版本。

此页包含多个平台和多个 Python 版本的下载内容:[设置 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步骤 2. 打开 Python 命令提示符

找到 SQL Server 使用的默认 Python 库位置。 如果已安装多个实例, 请找到要添加包的实例的 PYTHON_SERVICE 文件夹。

例如, 如果已使用默认值安装机器学习服务, 并且在默认实例上启用了机器学习, 则路径将如下所示:

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

打开与实例关联的 Python 命令提示符。

> [!TIP]
> 为了以后进行调试和测试, 你可能需要设置特定于实例库的 Python 环境。

### <a name="step-3-install-the-package-using-pip"></a>步骤 3. 使用 pip 安装包

+ 如果你习惯使用 Python 命令行, 请使用 PIP 安装新的包。 可以在`Scripts`子文件夹中找到**pip**安装程序。 

  SQL Server 安装程序不会将脚本添加到系统路径。 如果收到不能识别为`pip`内部或外部命令的错误, 可以在 Windows 中将 "脚本" 文件夹添加到 PATH 变量中。

  默认安装中 "**脚本**" 文件夹的完整路径如下:

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ 如果使用的是 visual studio 2017 或带有 Python 扩展的 visual studio 2015, 则可以从 " `pip install` **python 环境**" 窗口中运行。 单击 "**包**", 然后在 "文本" 框中提供要安装的包的名称或位置。 不需要键入`pip install`, 它会自动填充。 

    - 如果计算机可以访问 Internet, 请提供包的名称或特定包和版本的 URL。 
    
    例如, 若要安装 Windows 和 Python 3.5 支持的 CNTK 版本, 请指定下载 URL:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果计算机无法访问 internet, 则必须在开始安装之前下载 WHL 文件。 然后, 指定本地文件路径和名称。 例如, 粘贴以下路径和文件, 安装从站点下载的 WHL 文件:`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

系统可能会提示你提升权限以完成安装。

在安装过程中, 你可以在命令提示符窗口中看到状态消息:

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步骤 4. 将包或其函数作为脚本的一部分进行加载

安装完成后, 可以立即开始使用包, 如下一步所述。

有关使用 CNTK 的深度学习的示例, 请参阅以下教程:[用于 CNTK 的 Python API](https://cntk.ai/pythondocs/tutorials.html)

若要在脚本中使用包中的函数, 请在`import <package_name>`脚本的初始行中插入标准语句:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>使用 conda 列出已安装的包

可以通过不同的方式获取已安装包的列表。 例如, 你可以在 Visual Studio 的 " **Python 环境**" 窗口中查看已安装的包。

如果使用的是 Python 命令行, 则可以使用**Pip**或**conda**包管理器, 它包含在由 SQL Server 安装程序添加的 Anaconda Python 环境中。

1. 请参阅 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 右键单击 " **conda** > 以**管理员身份运行**", 然后按`conda list` enter 返回在当前环境中安装的包的列表。

1. 同样, 右键单击 " **.pip** > 以**管理员身份运行**", 然后输入`pip list`返回相同的信息。 

有关**conda**以及如何使用它来创建和管理多个 Python 环境的详细信息, 请参阅[使用 conda 管理环境](https://conda.io/docs/user-guide/tasks/manage-environments.html)。

> [!Note]
> SQL Server 安装程序不会将 Pip 或 Conda 添加到系统路径和生产 SQL Server 实例上, 因此, 从路径中保留非必要的可执行文件是最佳实践。 但对于开发和测试环境, 你可以将 "脚本" 文件夹添加到系统路径环境变量, 以从任何位置运行 Pip 和 Conda on 命令。
