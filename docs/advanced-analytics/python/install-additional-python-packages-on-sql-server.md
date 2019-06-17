---
title: 安装新的 Python 语言包-SQL Server 机器学习
description: 将新的 Python 包添加到 SQL Server 2017 机器学习服务 （数据库内） 和机器学习服务器 （独立版）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0c6c4384dd6c02e35fe77a6fb2bfc4017a445b1b
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140720"
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server 上安装新的 Python 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在 SQL Server 2017 机器学习服务的实例上安装新的 Python 包。 一般情况下，安装新的包的过程是类似于在标准的 Python 环境。 但是，执行一些其他步骤是必需的如果服务器不具有 internet 连接。

有关包的位置和安装路径的详细信息，请参阅[获取 R 或 Python 包信息](../package-management/installed-package-information.md)。

## <a name="prerequisites"></a>先决条件

+ [SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)使用 Python 语言选项。 

+ 包必须是 Windows 上的 Python 3.5 符合和运行。 

+ 安装包需要到服务器的管理访问权限。

## <a name="considerations"></a>注意事项

在将程序包添加之前, 请考虑包是否适用于 SQL Server 环境。 通常，数据库服务器是容纳多个工作负荷的共享的资产。 如果添加的服务器计算压力过多的包，性能将会受到影响。 

此外，某些常用的 Python 包 （如 Flask) 执行一些更适合的独立环境中的任务，例如 web 开发。 我们建议用于与数据库引擎，例如机器学习中受益的紧密集成的任务而不是只需查询数据库任务的 Python 中的数据库。

频繁地锁定数据库服务器。 在许多情况下，会完全阻止 Internet 访问。 对于具有一长串的依赖项包，您将需要提前识别这些依赖关系并愿意手动安装每个。

## <a name="add-a-new-python-package"></a>添加新的 Python 包

对于此示例中，我们假定你想要直接在 SQL Server 计算机上安装新包。

包安装是每个实例。 如果有多个实例的机器学习服务，你必须将包添加到每个。

在此示例中安装的包是[CNTK](https://docs.microsoft.com/cognitive-toolkit/)，一个用于从 Microsoft 支持自定义项，培训和共享的不同类型的神经网络的深度学习框架。

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步骤 1. 下载 Windows 版本的 Python 包

+ 如果没有 internet 访问的服务器上安装 Python 包，必须 WHL 文件下载到另一台计算机，然后将其复制到服务器。

    例如，在单独的计算机，你可以下载的 WHL 文件从该站点[ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)，然后将文件复制`cntk-2.1-cp35-cp35m-win_amd64.whl` 到 SQL Server 计算机上的本地文件夹。

+ SQL Server 2017 使用 Python 3.5。 

> [!IMPORTANT]
> 请确保获取包的 Windows 版本。 如果该文件中.gz 结束，则可能不是正确的版本。

此页包含下载为多个平台和多个 Python 版本：[设置 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步骤 2. 打开 Python 命令提示符

查找默认 Python 库位置中使用的 SQL Server。 如果已安装多个实例，找到你想要将包添加的实例的 PYTHON_SERVICE 文件夹。

例如，如果已安装机器学习服务使用默认值，并且在默认实例上启用机器学习，路径为，如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

打开 Python 命令提示符下，与实例相关联。

> [!TIP]
> 对于将来调试和测试，你可能想要设置特定于实例库的 Python 环境。

### <a name="step-3-install-the-package-using-pip"></a>步骤 3. 使用 pip 安装软件包

+ 如果您习惯于使用 Python 命令行，使用 PIP.exe 安装新的包。 您可以找到**pip**中的安装程序`Scripts`子文件夹。 

  SQL Server 安装程序不添加到系统路径的脚本。 如果收到错误`pip`未被识别为内部或外部命令，可以将脚本文件夹添加到 Windows 中的路径变量。

  完整路径**脚本**中默认安装文件夹是按如下所示：

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ 如果使用 Visual Studio 2017 或 Visual Studio 2015 使用 Python 扩展，则可以运行`pip install`从**Python 环境**窗口。 单击**包**，并在文本框中提供的名称或要安装的包的位置。 无需键入`pip install`; 它为你自动填充。 

    - 如果计算机具有 Internet 访问权限，提供包的名称或特定包和版本的 URL。 
    
    例如，若要安装的版本支持 Windows 和 Python 3.5 的 CNTK，指定的下载 URL: `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果计算机没有 internet 访问权限，必须在开始安装之前下载的 WHL 文件。 然后，指定的本地文件路径和名称。 例如，粘贴以下路径和要安装的 WHL 文件从站点下载文件： `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

系统可能提示您提升权限才能完成安装。

作为安装过程中，您可以看到在命令提示符窗口中的状态消息：

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步骤 4. 你的脚本的过程中加载包或其函数

安装完成后，您可以立即开始下一步中所述，使用包。

使用 CNTK 的深度学习的示例，请参阅以下教程：[Cntk Python API](https://cntk.ai/pythondocs/tutorials.html)

若要在脚本中使用包中的函数，插入标准`import <package_name>`语句中的脚本的初始行：

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>使用 conda 列出已安装包

有不同的方式，可以获取已安装的包的列表。 例如，可以查看已安装的包中**Python 环境**windows 的 Visual Studio。

如果使用 Python 命令行，则可以使用任一**Pip**或**conda**包管理器中，包括使用 SQL Server 安装程序添加的 Anaconda Python 环境。

1. 请转到 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 右键单击**conda.exe** > **以管理员身份运行**，然后输入`conda list`返回当前环境中安装的包列表。

1. 同样，用鼠标右键单击**pip.exe** > **以管理员身份运行**，然后输入`pip list`返回相同的信息。 

有关详细信息**conda**以及如何使用它来创建和管理多个 Python 环境，请参阅[管理使用 conda 环境](https://conda.io/docs/user-guide/tasks/manage-environments.html)。

> [!Note]
> SQL Server 安装程序不会添加 Pip 或 Conda 到系统路径和生产 SQL Server 实例上保持不必要置于路径之外的可执行文件是一种最佳做法。 但是，对于开发和测试环境，可以将脚本文件夹添加到系统 PATH 环境变量以从任何位置上命令运行 Pip 和 Conda。
