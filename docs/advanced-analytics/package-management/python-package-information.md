---
title: 获取 Python 包信息
description: 了解如何获取关于 SQL Server 机器学习服务上安装的 Python 包的信息（包括版本和安装位置）。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1aa12da4a138ea8f292fa8b64db00456d3c35fe3
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000447"
---
# <a name="get-python-package-information"></a>获取 Python 包信息

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何获取关于 SQL Server 机器学习服务上安装的 Python 包的信息（包括版本和安装位置）。 示例 Python 脚本显示如何列出安装路径和版本等包信息。

## <a name="default-python-library-location"></a>Python 库默认位置

使用 SQL Server 安装机器学习时，会在实例级别为安装的每种语言创建一个包库。 在 Windows 上，实例库是通过 SQL Server 注册的安全文件夹。

在 SQL Server 上的数据库内运行的所有脚本或代码都必须加载实例库中的函数。 SQL Server 无法访问安装到其他库的包。 这也适用于远程客户端：在服务器计算上下文中运行的任何 Python 代码只能使用实例库中安装的包。
若要保护服务器资产，只能由计算机管理员修改默认实例库。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python 的二进制文件的默认路径为：

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Python 的二进制文件的默认路径为：

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

这里假设默认 SQL 实例为 MSSQLSERVER。 如果将 SQL Server 安装作为用户定义的命名实例，则改用给定名称。

运行以下语句来验证当前实例的默认库。 此示例返回 Python `sys.path` 变量中包含的文件夹列表。 此列表包括当前目录和标准库路径。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

有关变量 `sys.path` 以及如何使用它为模块设置解释器搜索路径的详细信息，请参阅[模块搜索路径](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)。

## <a name="default-python-packages"></a>默认 Python 包

在安装过程中选择 Python 功能时，将随 SQL Server 机器学习服务一起安装以下 Python 包。

| 包 | 版本 |  描述 |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用于远程计算上下文、流式处理、并行执行进行数据导入和转换的 rx 函数、建模、可视化和分析。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 添加 Python 机器学习算法。 |

### <a name="component-upgrades"></a>组件升级

默认情况下，通过服务包和累积更新刷新 Python 包。 只能通过产品升级或将 Python 支持绑定到 Microsoft Machine Learning Server 来实现核心 Python 组件的其他包和完整版本升级。

有关详细信息，请参阅[升级 SQL Server 中的 R 和 Python 组件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-python-packages"></a>默认开放源代码 Python 包

如果安装过程中选择 Python 语言选项，则会安装 Anaconda 4.2 发行版 (Python 3.5)。 除 Python 代码库之外，标准安装还包括示例数据、单元测试和示例脚本。

> [!IMPORTANT]
> 切勿手动使用 Web 上的新版本覆盖 SQL Server 安装程序安装的 Python 版本。 Microsoft Python 包基于特定的 Anaconda 版本。 修改安装可能会使其不稳定。

## <a name="list-all-installed-python-packages"></a>列出所有已安装的 Python 包

以下示例脚本显示一组已安装的包及其版本。

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>查找单个 Python 包

如果已安装一个 Python 包并要确保它可用于特定的 SQL Server 实例，则可以执行存储过程来加载该包和返回消息。

例如，以下代码将查找 `scikit-learn` 包。
如果找到了该包，代码将返回消息“包 scikit-learn 已安装”。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pkg_resources.working_set], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

以下示例返回 revoscalepy 包和 Python 的版本。

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

+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [获取 R 包信息](r-package-information.md)
+ [安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)
+ [R 和 Python 教程](../tutorials/machine-learning-services-tutorials.md)
