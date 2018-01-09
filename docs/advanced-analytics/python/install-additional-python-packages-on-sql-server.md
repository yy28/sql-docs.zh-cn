---
title: "在 SQL Server 上安装新的 Python 包 |Microsoft 文档"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 78a76403f3212c7619afbf02577075161699fbd6
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>在 SQL Server 上安装新的 Python 软件包

本文介绍如何在 SQL Server 自 2017 年的实例上安装新的 Python 包。

它还说明如何列出在当前环境中安装的包。

## <a name="prerequisites"></a>必备条件

安装新包的过程很类似的标准 Python 环境中。 但是，执行一些其他步骤是必需的如果服务器没有 internet 连接。

+ 你必须已安装了机器学习服务 （数据库） 与 Python 语言选项。 有关说明，请参阅[设置 Python 机器学习服务](setup-python-machine-learning-services.md)。

+ 对于每个服务器实例，你必须安装包的单独副本。 包无法在实例之间共享。

+ 确定是否使用 Python 3.5 和 Windows 环境中，则你想要使用的包将起作用。 

    一般情况下，有几个限制上的包可以导入并在 SQL Server 环境中使用。 可能的问题包括在服务器或防火墙的情况，通过使用被阻止的网络功能的包或具有不在 Windows 计算机安装的依赖项包。

+ 到服务器的管理访问权限需要安装包。

## <a name="add-a-new-python-package"></a>添加一个新的 Python 包

对于此示例中，我们假定你想要直接在 SQL Server 计算机上安装新的包。

在此示例中安装的软件包是[CNTK](https://docs.microsoft.com/cognitive-toolkit/)，一个框架，用于从 Microsoft 支持自定义项，培训和不同类型的神经网络共享的深入学习。

> [!TIP]
> 需要配置你的 Python 工具的帮助？ 请参阅下列博客：
> 
> [开始使用 Python Web 服务使用机器学习服务器](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)
> 
> [David Crook: Microsoft 认知工具包 + VS Code](http://dacrook.com/cntk-vs-code-awesome/)

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>步骤 1. 下载 Windows 版本的 Python 包

+ 如果没有 internet 访问的服务器上安装 Python 包，必须将的 WHL 文件下载到另一台计算机，然后将其复制到服务器。

    例如，在单独的计算机，你可以下载的 WHL 文件从此站点[https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)，然后将文件复制`cntk-2.1-cp35-cp35m-win_amd64.whl`到 SQL Server 计算机上的本地文件夹。

+ SQL Server 2017 使用 Python 3.5。 请确保获取的 Windows 版本的包，以及使用 Python 3.5 兼容的版本。

此页包含多个平台和多个 Python 版本的下载：[设置 CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>步骤 2. 打开 Python 命令提示符

找到 SQL Server 使用的默认 Python 库位置。 如果已安装多个实例，请务必找到你想要将包添加的实例的 PYTHON_SERVICE 文件夹。

例如，如果已安装机器学习服务使用默认值，并且在默认实例上启用机器学习，该路径将为，如下所示：

    `C:\Program Files\Microsoft SQL  Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

打开与实例相关联 Python 命令提示符。

> [!TIP]
> 我们建议你在设置设置 Python 环境特定于机器学习 Server 或 SQL Server。

### <a name="step-3-install-the-package-using-pip"></a>步骤 3. 使用 pip 安装软件包

+ 如果你习惯于使用 Python 命令行，使用 PIP.exe 安装新包。 你可以找到**pip**中的安装程序`Scripts`子文件夹。 

    如果收到错误**pip**未识别为内部或外部命令，你可以将 Python 可执行文件和 Python 脚本文件夹的路径添加到 Windows 中的 PATH 变量。

    完整路径**脚本**默认安装中的文件夹是，如下所示：

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ 如果使用 Visual Studio 2017 或 Visual Studio 2015 使用的 Python 扩展，你可以运行`pip install`从**Python 环境**窗口。 单击**包**，并在文本框中提供的名称或要安装的包的位置。 你不需要键入`pip install`; 它为你自动填充。 

    - 如果计算机具有 Internet 访问，提供包，名称或特定包和版本的 URL。 例如，若要安装 Windows 和 Python 3.5 支持 CNTK 的版本，可以指定的下载 URL:`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 如果计算机没有 internet 访问权限，你应下载的 WHL 文件提前。 然后，指定本地文件路径和名称。 例如，粘贴以下路径和要安装的 WHL 文件从站点下载文件：`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

系统可能会提示你提升权限才能完成安装。

随着安装，您可以看到在命令提示符窗口的状态消息：

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```



### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>步骤 4. 你的脚本的一部分加载包或其函数

安装完成后，你可以立即开始使用包下, 一步中所述。

有关使用 CNTK，深入学习的示例，请参阅以下教程： [CNTK 的 Python API](https://cntk.ai/pythondocs/tutorials.html)

若要在脚本中使用包中的函数，插入标准`import <package_name>`脚本的初始行中的语句：

```python
import numpy as np
import cntk as cntk
cntk._version_
```

##  <a name="how-to-view-installed-packages-using-conda"></a>如何查看已安装的软件包使用 conda

有可以获取已安装的包列表的不同方法。 例如，你可以查看在已安装的软件包**Python 环境**的 Visual Studio 的 windows。

如果你使用 Python 命令行，则可以使用**conda**包管理器中，这是包含由 SQL Server 安装程序添加的 Anaconda Python 环境。

若要查看已安装在当前环境的 Python 包，请从命令提示符窗口运行以下命令：

```python
conda list
```

有关详细信息**conda**以及如何使用它来创建和管理多个 Python 环境，请参阅[管理具有 conda 环境](https://conda.io/docs/user-guide/tasks/manage-environments.html)。
