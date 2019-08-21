---
title: 获取 Python 包信息
description: 了解如何获取 SQL Server 机器学习服务上安装的 Python 包的相关信息, 包括版本和安装位置。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bccfc97fe75a718ce76ea0d1292bfc7ea6cb6564
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641174"
---
# <a name="get-python-package-information"></a>获取 Python 包信息

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何在 SQL Server 机器学习服务上获取有关已安装的 Python 包 (包括版本和安装位置) 的信息。 示例 Python 脚本说明了如何列出包信息, 如安装路径和版本。

## <a name="default-python-library-location"></a>默认 Python 库位置

如果使用 SQL Server 安装机器学习, 则会在实例级别为你安装的每种语言创建一个包库。 在 Windows 上, 实例库是 SQL Server 注册的安全文件夹。

在 SQL Server 上运行的所有脚本或代码都必须从实例库中加载函数。 SQL Server 无法访问安装到其他库的包。 这也适用于远程客户端: 在服务器计算上下文中运行的任何 Python 代码只能使用在实例库中安装的包。
若要保护服务器资产, 只能由计算机管理员修改默认实例库。

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
用于 Python 的二进制文件的默认路径为:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
用于 Python 的二进制文件的默认路径为:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

这假定为默认的 SQL 实例 MSSQLSERVER。 如果 SQL Server 作为用户定义的命名实例安装, 则改用给定的名称。

运行以下语句, 验证当前实例的默认库。 此示例返回 Python `sys.path`变量中包含的文件夹的列表。 此列表包括当前目录和标准库路径。

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

有关变量`sys.path`的详细信息以及如何使用它来设置模块的解释器搜索路径, 请参阅[模块搜索路径](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)。

## <a name="default-python-packages"></a>默认 Python 包

当你在安装过程中选择 Python 功能时, 将随 SQL Server 安装以下 Python 包机器学习服务。

| 包 | Version |  描述 |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 用于远程计算上下文、流式处理、用于数据导入和转换、建模、可视化和分析的 rx 函数的并行执行。 |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | 在 Python 中添加机器学习算法。 |

### <a name="component-upgrades"></a>组件升级

默认情况下, Python 包通过 service pack 和累积更新进行刷新。 仅通过产品升级或将 Python 支持绑定到 Microsoft Machine Learning Server, 才能实现核心 Python 组件的其他包和完整版本升级。

有关详细信息, 请参阅[SQL Server 中的升级 R 和 Python 组件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-python-packages"></a>默认的开源 Python 包

当你在安装过程中选择 Python 语言选项时, 将安装 Anaconda 4.2 分发 (覆盖 Python 3.5)。 除了 Python 代码库以外, 标准安装还包括示例数据、单元测试和示例脚本。

> [!IMPORTANT]
> 切勿手动覆盖 SQL Server 安装程序安装了 web 上的更新版本。 Microsoft Python 包基于 Anaconda 的特定版本。 修改安装会使其不稳定。

## <a name="list-all-installed-python-packages"></a>列出所有已安装的 Python 包

该`pip`模块是默认安装的, 除了支持标准 Python 支持的程序包之外, 还支持使用许多操作来列出已安装的包。 可以从 Python `pip`命令提示符运行, 但也可以从`sp_execute_external_script`调用某些 pip 函数。

下面的示例脚本显示已安装包及其版本的列表。

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
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>查找单个 Python 包

如果已安装 Python 包, 并且想要确保它可用于特定的 SQL Server 实例, 则可以执行存储过程以加载包并返回消息。

例如, 以下代码将查找`scikit-learn`包。
如果找到了包, 则代码将返回消息 "包 scikit-learn-已安装"。

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pip
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

下面的示例返回 revoscalepy 包和 Python 的版本。

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
