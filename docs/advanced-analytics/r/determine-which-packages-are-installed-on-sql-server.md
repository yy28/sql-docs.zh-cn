---
title: 获取有关 SQL Server 机器学习的 R 和 Python 包信息 |Microsoft 文档
description: 确定 R 和 Python 包版本，验证安装，并获取 SQL Server R Services 或机器学习服务上的安装程序包的列表。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 21975b4a59cbfaf1e3a203bc732543144856633f
ms.sourcegitcommit: df382099ef1562b5f2d1cd506c1170d1db64de41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
#  <a name="get-r-and-python-package-information-on-sql-server"></a>Get R 和 SQL Server 上的 Python 包信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有时当您正在使用多个环境或 R 或 Python 的安装，你需要验证你正在运行的代码对。 Python，或正确的工作区中使用了预期的环境例如，如果你已升级机器学习使用绑定的组件，R 库路径可能是而不是默认的其他文件夹中。 另外，如果你安装 R 客户端或独立服务器实例，你可能有多个 R 库您的计算机上。

这篇文章中的示例演示如何获取的路径和版本的 SQL Server 正在使用的库。

## <a name="get-the-current-r-library"></a>获取当前的 R 库

有关**R**在任何版本的 SQL Server，运行以下语句以验证当前实例的默认库：

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

或者，你可以在新版本的 SQL Server 自 2017 年 1 机器学习 Services 中的 RevoScaleR 使用 rxSqlLibPaths 或[R Services 升级后 R 到在最低 RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 此存储的过程返回实例库的路径和版本的 SQL Server 使用 RevoScaleR:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函数可以只能在本地计算机上执行。 该函数不能返回为远程连接的库路径。

**结果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-current-python-library"></a>获取当前的 Python 库

有关**Python**在 SQL Server 自 2017 年，运行以下语句以验证当前实例的默认库。 此示例返回的 Python 中包含的文件夹列表`sys.path`变量。 该列表包括当前目录和标准库路径。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**结果**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

有关变量的详细信息`sys.path`以及如何使用它来设置的模块的解释程序的搜索路径，请参阅[Python 文档](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>列出所有包

有多种方法，你可以获取当前安装的包的完整列表。 运行中的包列表命令从 sp_execute_external_script 的一个优点是，则可保证要从中获取安装在实例库中的程序包。

### <a name="r"></a>R

下面的示例使用 R 函数`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]存储过程来获取的已安装在当前实例的 R_SERVICES 库的包的矩阵。 此脚本返回描述文件中的包名称和版本字段，则返回仅名称。

```SQL
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

有关可选信息和 R 包描述字段的默认字段，请参阅[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模块默认情况下，安装和支持对于列表安装包，除了支持标准 Python 的许多操作。 你可以运行`pip`Python 从命令提示符下，当然，但你还可以调用某些 pip 函数从`sp_execute_external_script`。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

运行时`pip`从命令行中，有许多其他有用的功能：`pip list`获取已安装的所有包，而`pip freeze`列出安装的包`pip`，并不列出 pip 本身的包依赖于。 你还可以使用`pip freeze`生成依赖项文件。

## <a name="find-a-single-package"></a>查找单个包

如果你已安装了包，并想要确保它是对特定的 SQL Server 实例可用，则可以执行以下的存储的过程调用，以将包加载，并且返回仅消息。

### <a name="r"></a>R

本示例查找并加载 RevoScaleR 库中，如果可用。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到包，则返回一条消息:"命令已成功完成。"

+ 如果无法找到或加载包，可能会包含文本时出错:"没有名为 MissingPackageName 程序包"

### <a name="python"></a>Python

可以从 Python 执行 Python 等效检查 shell，使用`conda`或`pip`命令。 或者，在存储过程中运行此语句：

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="get-package-information-in-r-and-python-tools"></a>在 R 和 Python tools 中获取包信息

所有前面的步骤假定你使用的 SQL Server 工具如 Management Studio (SSMS)。 如果你愿意使用 R 和 Python 的工具，下面的说明解释如何从 R 或 Python 的命令行获取库和包的信息。

### <a name="r-commands"></a>R 命令

R 实例库是 files\microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\library。

启动从这些位置，以确保包实例库中的使用的标准 R 工具：

+ \MSSQL14。MSSQLSERVER\R_SERVICES\bin\R.exe 的 R 命令提示符
+ \MSSQL14。MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe R 控制台应用程序

你可以使用标准 R 命令或 RevoScaleR 命令以获取包信息。 自动加载 RevoScaleR 包。 

返回 RevoScaleR 包信息：

    > print(Revo.version)

返回所有已安装的软件包的列表：

    > installed.packages()

返回： 的版本

    > packageDescription("base")

### <a name="python-commands"></a>Python 命令

Python 支持仅 SQL Server 自 2017 年。 用于 Python 的实例库是 files\microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\。

从该位置，以确保使用实例库中的包打开 Python 命令窗口：

+ \MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Python.exe

打开交互式帮助：

    > help()

模块名称提示符处键入帮助以获取包的内容、 版本和文件位置：

    help> revoscalepy

<a name="pip-conda"></a>

### <a name="python-package-managers-pip-and-conda"></a>Python 包管理器 （Pip 和 Conda）

Anaconda 包含用于管理包的 Python 工具。 在默认实例、 Pip、 Conda 和其他工具都可以位于 files\microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts。

SQL Server 安装程序不会添加 Pip 或保持非基本可执行文件从路径的 Conda 到系统路径和在生产 SQL Server 实例中，是一种最佳做法。 但是，对于开发和测试环境，无法将脚本文件夹添加到系统 PATH 环境变量以在命令上运行 Pip 和 Conda，从任何位置。

1. 请转到 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 右键单击**conda.exe** > **以管理员身份运行**，并输入`conda list`以返回在当前环境中安装的包的列表。

1. 同样，右键单击**pip.exe** > **以管理员身份运行**，并输入`pip list`返回相同信息。 


## <a name="next-steps"></a>后续步骤

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)