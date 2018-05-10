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
ms.openlocfilehash: 3295bbdbb00c73c9aaa37dcb15d35121b82454bb
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
#  <a name="get-r-and-python-package-information-on-sql-server-machine-learning"></a>获取有关 SQL Server 机器学习的 R 和 Python 包信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

如果你已安装多个 Python 环境，或使用多个 R 工具，很容易包安装到的错误的库或环境，然后不能以更高版本查找。 本文提供了查询和指南适用于 determininga 包版本，以及若要列出在当前的 SQL Server 环境中安装的包。

## <a name="verify-the-current-default-library"></a>验证当前的默认库

有关**R**在 SQL Server 中，运行以下语句以验证当前实例的默认库：

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

有关**Python**在 SQL Server 中，运行以下语句以验证当前实例的默认库：

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>生成使用存储的过程的包列表

有多种方法，你可以获取当前安装的包的完整列表。 运行中的包列表命令从 sp_execute_external_script 的一个优点是，则可保证要从中获取安装在实例库中的程序包。

### <a name="r"></a>R

下面的示例使用 R 函数`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]存储过程来获取的已安装在当前实例的 R_SERVICES 库的包的矩阵。 为避免分析 DESCRIPTION 文件中的字段，仅返回了名称。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

有关可选信息和 R 包描述字段的默认字段，请参阅[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模块默认情况下，安装和支持对于列表安装包，除了支持标准 Python 的许多操作。 你可以运行`pip`Python 从命令提示符下，当然，但你还可以调用某些 pip 函数从`sp_execute_external_script`。

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

运行时`pip`从命令行中，有许多其他有用的功能：`pip list`获取已安装的所有包，而`pip freeze`列出安装的包`pip`，并不列出 pip 本身的包依赖于。 你还可以使用`pip freeze`生成依赖项文件。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>验证是否使用实例安装包

如果你已安装了包，并想要确保它是对特定的 SQL Server 实例可用，则可以执行以下的存储的过程调用，以将包加载，并且返回仅消息。

### <a name="r"></a>R

本示例查找并加载 RevoScaleR 库中，如果可用。

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ 如果找到包，则返回一条消息:"命令已成功完成。"

+ 如果无法找到或加载包，可能会包含文本时出错:"没有名为 MissingPackageName 程序包"

### <a name="python"></a>Python

可以从 Python 执行 Python 等效检查 shell，使用`conda`或`pip`命令。 或者，在存储过程中运行此语句：

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>查看使用的实用程序或 IDE 的安装的包

大多数开发工具提供的对象浏览器或已安装或已在当前工作区或环境中加载的包的列表。 本部分提供关于使用受欢迎的 R 或 Python 工具短的一些提示。

### <a name="r-tools"></a>R 工具

有多种方式来获取使用 R 实用程序的安装或加载包的列表。 

+ 从本地 R 实用程序，使用基础 R 函数，如`installed.packages()`中, 附带`utils`包。 若要获取的实例的准确列表，您必须显式指定的库路径或使用与实例库关联的 R 工具。

### <a name="python-tools"></a>Python 工具

Visual Studio 的 Python 扩展让你十分方便，若要查看安装在当前环境中，或其他 IDE 中列出的虚拟环境中的包。 你可以配置多个环境、 从列表中，选择环境和查看包或将新包安装到该环境。

+ [Python 环境](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Visual Studio 代码是使用多个可用的 Python linters 支持 Python 的免费编辑器。 虽然 VS Code 不提供包浏览器与 Visual Studio 中的一样，它支持配置和多个环境之间切换。

+ [在 Visual Studio 代码中的 Python](https://code.visualstudio.com/docs/languages/python)

一些额外的配置可能需要运行**revoscalepy**从远程客户端的命令：

+ [在 Windows 上本地安装自定义 Python 包和解释程序](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

此博客提供了一些配置包括 PyCharm，要使用其他 Python 环境的有用提示**revoscalepy**。

+ [要开始使用 Python Web 服务使用机器学习服务器](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>使用从机器学习服务器函数

因为用于 SQL Server 支持执行从远程客户端的代码的库，你可以使用这些函数来找出哪些包安装在远程环境中。

### <a name="revoscaler"></a>RevoScaleR

如果在远程客户端中工作，但没有对服务器的访问，你仍可以获取使用 RevoScaleR 函数来安装在 SQL Server 的包的列表。 作为计算上下文，这需要有权连接到服务器指定的 SQL Server。 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)发现远程计算上下文中的包的路径。

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)获取有关计算上下文中安装的程序包的信息。

例如，运行下面的 R 代码，以获取指定的 SQL Server 计算上下文中提供的程序包的列表。

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

下面的示例获取在本地计算上下文中，以及程序包版本 RevoScaleR 的库位置。

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

类似于 RevoScaleR 函数此时不可用。 在更高版本中查找它们**revoscalepy**。

## <a name="get-library-location-and-version"></a>获取库位置和版本

有时当您正在使用多个环境或 R 或 Python 的安装，你需要验证你正在运行的代码对。 Python，或正确的工作区中使用了正确的环境

例如，如果你已升级机器学习使用绑定的组件，R 库路径可能是而不是默认的其他文件夹中。 另外，如果你安装 R 客户端或独立服务器实例，你可能有多个 R 库您的计算机上。

这些示例演示如何获取的路径和版本的 SQL Server 正在使用的库。

### <a name="r"></a>R

此存储的过程返回的路径实例库，以及 SQL Server 使用 RevoScaleR 包的版本：

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函数可以只能在目标计算机上执行。 该函数不能返回为远程连接的库路径。

**结果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

此示例返回的 Python 中包含的文件夹列表`sys.path`变量。 该列表包括当前目录和标准库路径。

```sql
EXEC sp_execute_external_script
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

