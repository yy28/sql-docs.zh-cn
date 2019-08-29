---
title: 安装具有 pip 的 Python 包
description: 了解如何使用 Python pip 在 SQL Server 机器学习服务的实例上安装新的 Python 包。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: dc5addca9c9bbf01408cea89f85676813b97506c
ms.sourcegitcommit: 52d3902e7b34b14d70362e5bad1526a3ca614147
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70109758"
---
# <a name="install-python-packages-with-sqlmlutils"></a>通过 sqlmlutils 安装 Python 包

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何使用[**sqlmlutils**](https://github.com/Microsoft/sqlmlutils)包中的函数将新的 Python 包安装到 SQL Server 机器学习服务的实例。 安装的包可用于在使用 T-sql [sp-](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) -----------------------------------

有关包位置和安装路径的详细信息, 请参阅[获取 Python 包信息](../package-management/python-package-information.md)。

> [!NOTE]
> 不建议在`pip install` SQL Server 上添加 Python 包标准 Python 命令。 请改用本文中所述的**sqlmlutils** 。

## <a name="prerequisites"></a>先决条件

+ 必须使用 Python 语言选项安装[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)。

+ 在用于连接到 SQL Server 的客户端计算机上安装[python](https://www.python.org/) 。 你还可能需要使用[Python 扩展](https://marketplace.visualstudio.com/items?itemName=ms-python.python)的 python 开发环境, 如[Visual Studio Code](https://code.visualstudio.com/download) 。 

+ 在用于连接到 SQL Server 的客户端计算机上安装[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is)或[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)。 您可以使用其他数据库管理或查询工具, 但本文假定 Azure Data Studio 或 SSMS。

### <a name="other-considerations"></a>其他注意事项

+ 包必须符合 Python 3.5 标准并在 Windows 上运行。

+ Python 包库位于 SQL Server 实例的 Program Files 文件夹中, 默认情况下, 安装在此文件夹中需要管理员权限。 有关详细信息, 请参阅[包库位置](../package-management/python-package-information.md#default-python-library-location)。

+ 包安装按实例进行。 如果有多个机器学习服务实例, 则必须将包添加到每个实例中。

+ 添加包之前, 请考虑包是否适合 SQL Server 环境。

  + 建议你使用 Python 数据库中的任务, 这些任务受益于与数据库引擎 (如机器学习) 的紧密集成, 而不是只查询数据库的任务。

  + 如果添加的包在服务器上施加了太多的计算压力, 性能将会降低。

  + 在强化的 SQL Server 环境中, 你可能需要避免以下情况:
    + 需要网络访问的包
    + 需要提升文件系统访问权限的包
    + 用于 web 开发或其他任务的包, 这些包不能通过在 SQL Server 内部运行

## <a name="install-sqlmlutils-on-the-client-computer"></a>在客户端计算机上安装 sqlmlutils

若要使用**sqlmlutils**, 首先需要将其安装在用于连接 SQL Server 的客户端计算机上。

1. 从 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist 下载最新的**sqlmlutils** zip 文件到客户端计算机。 请勿解压缩文件。

1. 打开**命令提示符**并运行以下命令, 安装**sqlmlutils**包。 替换下载的**sqlmlutils** zip 文件的完整路径-本示例假定下载的文件是`c:\temp\sqlmlutils_0.6.0.zip`。

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>SQL Server 上添加 Python 包

在下面的示例中, 你将把[文本工具](https://pypi.org/project/text-tools/)包添加到 SQL Server。

### <a name="add-the-package-online"></a>联机添加包

如果用于连接到 SQL Server 的客户端计算机具有 Internet 访问权限, 则可以使用**sqlmlutils**通过 internet 查找**文本工具**包和任何依赖项, 然后远程将包安装到 SQL Server 实例。

1. 在客户端计算机上, 打开**python**或 python 环境。

1. 使用以下命令安装**文本工具**包。 替换为您自己的 SQL Server 数据库连接信息。

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>脱机添加包

如果用于连接 SQL Server 的客户端计算机没有 Internet 连接, 则可以在具有 Internet 访问权限的计算机上使用**pip** , 以将包和任何依赖包下载到本地文件夹。 然后, 将该文件夹复制到客户端计算机, 您可以在其中脱机安装包。

#### <a name="on-a-computer-with-internet-access"></a>在能够访问 Internet 的计算机上

1. 打开**命令提示符**并运行以下命令, 以创建一个包含**文本工具**包的本地文件夹。 此示例将创建文件夹`c:\temp\text-tools`。

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. `text-tools`将文件夹复制到客户端计算机。 下面的示例假定已将其复制`c:\temp\packages\text-tools`到。

#### <a name="on-the-client-computer"></a>在客户端计算机上

使用**sqlmlutils**安装在**pip**创建的本地文件夹中找到的每个包 (WHL 文件)。 安装包的顺序并不重要。

在此示例中,**文本工具**没有依赖项, 因此该`text-tools`文件夹中只有一个文件可供安装。 与此相反, 包 (如**scikit-learn** ) 具有11个依赖项, 因此你可以在文件夹中找到12个文件 ( **scikit-learn**包和11个相关包), 然后安装每个文件。

运行以下 Python 脚本。 替换为您自己的 SQL Server 数据库连接信息, 以及包的实际文件路径和名称。 对文件夹中的每个包文件重复执行语句。`sqlmlutils.SQLPackageManager`

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>在 SQL Server 中使用包

你现在可以在 SQL Server 的 Python 脚本中使用包。 例如：

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>从 SQL Server 中删除包

如果要删除**文本工具包**, 请在客户端计算机上使用之前定义的相同连接变量使用以下 Python 命令。

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>请参阅

+ 若要查看 SQL Server 机器学习服务中安装的 Python 包的相关信息, 请参阅[获取 Python 包信息](../package-management/python-package-information.md)。

+ 有关 SQL Server 机器学习服务中安装 R 包的信息, 请参阅[SQL Server 上安装新的 r 包](../r/install-additional-r-packages-on-sql-server.md)。
