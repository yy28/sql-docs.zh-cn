---
title: 获取 R 和 Python 包信息
description: 确定 R 和 Python 包版本, 验证安装, 并获取 SQL Server R Services 或机器学习服务上已安装包的列表。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: cec029f4ffb047a49ff9902c430c4bd98aa03850
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470290"
---
#  <a name="get-r-and-python-package-information"></a>获取 R 和 Python 包信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

有时, 当使用多个环境或 R 或 Python 的安装时, 需要验证正在运行的代码是使用适用于 Python 的预期环境还是适用于 R 的正确工作区。例如, 如果已[升级 r 或 Python](../install/upgrade-r-and-python.md), 则 r 库的路径可能位于不同于默认的文件夹中。 此外, 如果您安装了 R 客户端或独立服务器的实例, 则您的计算机上可能有多个 R 库。

本文介绍了如何获取 SQL Server 所使用的包的路径和版本。

## <a name="get-the-r-library-location"></a>获取 R 库位置

对于任何版本的 SQL Server, 请运行以下语句来验证当前实例的默认 R 包库:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

(可选) 可以在较新版本的 RevoScaleR 中使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) , SQL Server 2017 机器学习服务或[r Services 至少升级 r 到 RevoScaleR 9.0.1](../install/upgrade-r-and-python.md)。 此存储过程返回 SQL Server 使用的实例库路径和 RevoScaleR 的版本:

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
> [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)函数只能在本地计算机上执行。 函数无法返回远程连接的库路径。

**结果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>获取 Python 库位置

对于 SQL Server 2017 中的**Python** , 请运行以下语句来验证当前实例的默认库。 此示例返回 Python `sys.path`变量中包含的文件夹的列表。 此列表包括当前目录和标准库路径。

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

有关变量`sys.path`的详细信息以及如何使用它来设置模块的解释器搜索路径, 请参阅[Python 文档](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>列出所有包

可以通过多种方法获取当前安装的包的完整列表。 从 sp_execute_external_script 运行包列表命令的一个优点是, 可以确保在实例库中安装包。

### <a name="r"></a>R

下面的示例使用`installed.packages()` [!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程中的 R 函数来获取已在 R_SERVICES 库中为当前实例安装的包的矩阵。 此脚本返回描述文件中的 "包名称" 和 "版本" 字段, 只返回名称。

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

有关 R 包说明字段的可选字段和默认字段的详细信息, 请参阅[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

### <a name="python"></a>Python

默认`pip`情况下将安装此模块, 并且除了标准 Python 支持的程序包之外, 还支持许多用于列出已安装包的操作。 当然, 您`pip`可以从 Python 命令提示符运行, 但也可以从`sp_execute_external_script`调用某些 pip 函数。

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

在命令`pip`行中运行时, 有许多其他有用函数: `pip list`获取已安装的所有包, 而`pip freeze`列出安装`pip`的包, 并且不列出 pip 本身的包依赖于。 你还可以使用`pip freeze`来生成依赖项文件。

## <a name="find-a-single-package"></a>查找单个包

如果已安装了包, 并且想要确保它可用于特定的 SQL Server 实例, 则可以执行以下存储过程调用来加载包并仅返回消息。

### <a name="r"></a>R

此示例查找并加载 RevoScaleR 库 (如果可用)。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 如果找到了包, 则返回一条消息:"命令已成功完成。"

+ 如果找不到或无法加载包, 则会收到包含以下文本的错误: "没有名为 ' MissingPackageName ' 的包"

### <a name="python"></a>Python

可以使用`conda`或`pip`命令从 python shell 执行等效的 python 检查。 或者, 在存储过程中运行以下语句:

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

你可以使用 Management Studio 获取 R 和 Python 包版本信息。

### <a name="r-package-version"></a>R 包版本

此语句返回 RevoScaleR 包版本和基础 R 版本。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 包版本

此语句返回 revoscalepy 包版本和 Python 版本。

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

+ [安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [教程、示例、解决方案](../tutorials/machine-learning-services-tutorials.md)