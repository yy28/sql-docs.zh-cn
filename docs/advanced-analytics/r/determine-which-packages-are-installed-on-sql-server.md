---
title: 获取 R 和 Python 包信息-SQL Server 机器学习服务
description: 确定 R 和 Python 包版本中，验证安装，并获取 SQL Server R Services 或机器学习服务上已安装的包的列表。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/08/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3e7dd580cd7d03235be704a7c46e5171a6526ae8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506224"
---
#  <a name="get-r-and-python-package-information"></a>获取 R 和 Python 包信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

有时当您正在使用多个环境或 R 或 Python 的安装，您需要验证正在运行的代码使用预期的环境的 Python 或正确的工作区为。例如，如果你已升级的机器学习通过组件[绑定](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)，R 库的路径可能不同于默认文件夹中。 另外，如果在安装 R 客户端或独立服务器实例，您可能有多个 R 库在计算机上。

在本文中的 R 和 Python 脚本示例演示了如何获取的路径和版本的 SQL Server 使用的包。

## <a name="get-the-r-library-location"></a>获取 R 库位置

有关 SQL Server 任何版本，运行以下语句以验证[默认 R 包库](installing-and-managing-r-packages.md)的当前实例：

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

（可选） 可以使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)较新版本的 SQL Server 2017 机器学习服务中的 RevoScaleR 中或[R Services 至少升级到 R RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 此存储的过程返回的实例库路径和 RevoScaleR SQL Server 使用的版本：

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
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)可以仅在本地计算机上执行函数。 该函数不能返回为远程连接的库路径。

**结果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>获取 Python 库位置

有关**Python**在 SQL Server 2017 中，运行以下语句以验证当前实例的默认库。 此示例返回在 Python 中所包括的文件夹列表`sys.path`变量。 此列表包括当前目录，以及标准库路径。

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

有关变量的详细信息`sys.path`它用于设置解释器的搜索路径的模块，请参阅[Python 文档](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>列出所有包

有多种方法可获取当前安装的包的完整列表。 运行中的包列表命令从 sp_execute_external_script 的一个优点是可以保证以获取实例库中安装的包。

### <a name="r"></a>R

下面的示例使用 R 函数`installed.packages()`在[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程来获得的当前实例的 R_SERVICES 库中已安装的包的矩阵。 此脚本返回说明文件中的包名称和版本字段，将返回仅名称。

```sql
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

有关详细信息的可选和默认字段的 R 包说明字段，请参阅[ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

`pip`模块默认情况下，安装并支持列表安装包，除了支持标准 Python 的许多操作。 你可以运行`pip`Python 从命令提示符下，当然，但您还可以调用某些 pip 函数从`sp_execute_external_script`。

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

运行时`pip`从命令行中，有许多其他有用的功能：`pip list`获取安装的所有包，而`pip freeze`列出了安装的包`pip`，并不会列出 pip 本身的包取决于。 此外可以使用`pip freeze`生成依赖项文件。

## <a name="find-a-single-package"></a>查找单个包

如果你已安装了包，并想要确保其可供特定的 SQL Server 实例，可以执行以下的存储的过程调用，以将包加载，并且返回仅消息。

### <a name="r"></a>R

此示例中查找并加载 RevoScaleR 库中，如果可用。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到包，则返回一条消息："命令已成功完成"。

+ 如果无法找到或加载包，可能会包含文本时出错:"没有名为 MissingPackageName 程序包"

### <a name="python"></a>Python

可以从 Python 执行等效检查适用于 Python shell，使用`conda`或`pip`命令。 或者，在存储过程中运行此语句：

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

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>获取包版本

可以获取 R 和 Python 包使用 Management Studio 的版本信息。

### <a name="r-package-version"></a>R 包版本

此语句返回的 RevoScaleR 包版本和基本的 R 版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 包版本

此语句返回 revoscalepy 包版本和版本的 Python。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
'
```

## <a name="next-steps"></a>后续步骤

+ [安装新 R 包](install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)