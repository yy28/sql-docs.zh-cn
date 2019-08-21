---
title: 获取 R 包信息
description: 了解如何 SQL Server 机器学习服务和 SQL Server R Services 获取有关已安装的 R 包的信息。
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641154"
---
# <a name="get-r-package-information"></a>获取 R 包信息

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何在 SQL Server 机器学习服务和 SQL Server R Services 获取有关已安装的 R 包的信息。 示例 R 脚本向您演示如何列出包信息, 如安装路径和版本。

## <a name="default-r-library-location"></a>默认 R 库位置

如果使用 SQL Server 安装机器学习, 则会在实例级别为你安装的每种语言创建一个包库。 在 Windows 上, 实例库是 SQL Server 注册的安全文件夹。

在 SQL Server 上运行的所有脚本都必须从实例库中加载函数。 SQL Server 无法访问安装到其他库的包。 这也适用于远程客户端: 在服务器计算上下文中运行的任何 R 脚本只能使用在实例库中安装的包。
若要保护服务器资产, 只能由计算机管理员修改默认实例库。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R 的二进制文件的默认路径为:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R 的二进制文件的默认路径为:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
R 的二进制文件的默认路径为:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

这假定为默认的 SQL 实例 MSSQLSERVER。 如果 SQL Server 作为用户定义的命名实例安装, 则改用给定的名称。

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

运行以下语句, 验证当前实例的默认 R 包库:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

以下语句使用[rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)来返回 SQL Server 使用的 RevoScaleR 实例的路径和版本:

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

## <a name="default-r-packages"></a>默认 R 包

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

以下 R 包随 SQL Server R Services 一起安装。

|包 | Version | 描述 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 用于远程计算上下文、流式处理、用于数据导入和转换、建模、可视化和分析的 rx 函数的并行执行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 用于在存储过程中包含 R 脚本。 |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

当你在安装过程中选择 R 功能时, 将随 SQL Server 安装以下 R 包机器学习服务。

|包 | Version | 描述 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | 用于远程计算上下文、流式处理、用于数据导入和转换、建模、可视化和分析的 rx 函数的并行执行。 |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | 用于在存储过程中包含 R 脚本。 |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | 在 R 中添加机器学习算法。 | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | 用于在 R 中编写 MDX 语句。 |

::: moniker-end

### <a name="component-upgrades"></a>组件升级

默认情况下, R 包通过 service pack 和累积更新进行刷新。 核心 R 组件的其他包和完整版本升级只能通过产品升级或通过将 R 支持绑定到 Microsoft Machine Learning Server 来实现。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
此外, 还可以通过组件升级向 SQL Server 实例添加 MicrosoftML 和 olapR 包。
::: moniker-end

有关详细信息, 请参阅[SQL Server 中的升级 R 和 Python 组件](../install/upgrade-r-and-python.md)。

## <a name="default-open-source-r-packages"></a>默认的开源 R 包

R 支持包括开源, 因此你可以调用基本 R 函数并安装其他开源和第三方包。 R 语言支持包括**基本**、**统计**、 **utils**等核心功能。 R 的基本安装还包括多个示例数据集和标准 R 工具, 例如**rgui.exe** (一种轻型交互式编辑器) 和**rterm.exe** (R 命令提示符)。

安装中包含的开源 R 的分发是[Microsoft R open (MRO)](https://mran.microsoft.com/open)。 MRO 通过包含附加开源包 (如[Intel 数学内核库](https://en.wikipedia.org/wiki/Math_Kernel_Library)), 将值添加到基本 R。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用 SQL Server R Services 安装程序的 MRO 提供的 R 版本为3.2.2。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用 SQL Server 机器学习服务安装程序的 MRO 提供的 R 版本为3.3.3。
::: moniker-end

> [!IMPORTANT]
> 切勿手动覆盖通过 web 上的更新版本 SQL Server 安装程序安装的 R 版本。 Microsoft R 包基于特定版本的 R。修改安装可能会使其不稳定。

## <a name="list-all-installed-r-packages"></a>列出所有已安装的 R 包

下面的示例使用`installed.packages()` [!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程中的 r 函数来显示已安装在当前 SQL 实例的 R_SERVICES 库中的 r 包的列表。 此脚本返回说明文件中的 "包名称" 和 "版本" 字段。

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

有关 R 包说明字段的可选字段和默认字段的详细信息, 请参阅[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

## <a name="find-a-single-r-package"></a>查找单个 R 包

如果你已安装了 R 包, 并且想要确保它可用于特定的 SQL Server 实例, 则可以执行存储过程以加载包并返回消息。

例如, 下面的语句查找并加载[粘连](https://cran.r-project.org/web/packages/glue/)包 (如果可用)。
如果找不到或无法加载包, 则会收到一个错误, 其中包含文本 "没有名为 ' 胶水 ' 的包"。

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

若要查看有关包的详细信息, 请`packageDescription`查看。
以下语句返回**粘连**包的信息。

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>后续步骤

+ [安装新 R 包](../r/install-additional-r-packages-on-sql-server.md)
+ [获取 Python 包信息](python-package-information.md)
+ [安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)
+ [R 和 Python 教程](../tutorials/machine-learning-services-tutorials.md)
