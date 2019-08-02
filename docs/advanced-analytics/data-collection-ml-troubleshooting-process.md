---
title: 机器学习的数据收集疑难解答
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7566d9b25b15a334e48380daca6cb81e92f6a2b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715231"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>机器学习的数据收集疑难解答

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍了尝试自行解决问题时应使用的数据收集方法, 或与 Microsoft 客户支持部门的帮助。

## <a name="sql-server-version-and-edition"></a>SQL Server 版本和版本

SQL Server 2016 R Services 是 SQL Server 的第一版, 包括集成的 R 支持。 SQL Server 2016 Service Pack 1 (SP1) 包含多项重大改进, 包括运行外部脚本的能力。 如果你使用的是 SQL Server 2016, 你应考虑安装 SP1 或更高版本。

SQL Server 2017 及更高版本具有 Python 语言集成。 无法在早期版本中获取 Python 功能集成。

若要获取版本和版本的帮助, 请参阅此文, 其中列出了每个[SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)的生成号。

根据你使用的 SQL Server 版本, 某些机器学习功能可能不可用或受到限制。 以下文章列出了企业版、开发人员版、标准版和速成版中的机器学习功能。

* [SQL Server 的版本和支持的功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R 和 Python 功能 (按版本) SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 语言和工具版本

通常, 在选择 R Services 功能或机器学习服务功能时安装的 Microsoft R 版本由 SQL Server 的内部版本号决定。 如果升级或修补 SQL Server, 则还必须升级或修补其 R 组件。

有关版本和 R 组件下载的链接的列表, 请参阅在[不访问 internet 的情况下安装机器学习组件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在具有 internet 访问权限的计算机上, 会自动标识和安装所需的 R 版本。

在称为绑定的进程中, 可以从 SQL Server 数据库引擎单独升级 R Server 组件。 因此, 在 SQL Server 中运行 R 代码时使用的 R 版本可能会有所不同, 这取决于安装的 SQL Server 版本以及是否将服务器迁移到最新的 R 版本。

### <a name="determine-the-r-version"></a>确定 R 版本

确定 R 版本的最简单方法是通过运行如下语句来获取运行时属性:

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> 如果 R Services 不起作用, 请尝试仅运行 Rgui.exe 中的 R 脚本部分。

作为最后的手段, 您可以打开服务器上的文件以确定安装的版本。 为此, 请找到 rlauncher 文件以获取 R 运行时和当前工作目录的位置。 建议你创建并打开该文件的副本, 以便不会意外更改任何属性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要获取 R 版本和 RevoScaleR 版本, 请打开一个 R 命令提示符, 或打开与实例关联的 Rgui.exe。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 控制台在启动时显示版本信息。 例如, 以下版本表示 SQL Server 2017 的默认配置:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 版本

可以通过多种方式来获取 Python 版本。 最简单的方法是从 Management Studio 或任何其他 SQL 查询工具运行此语句:

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

如果机器学习服务未运行, 则可以通过查看 pythonlauncher 文件来确定安装的 Python 版本。 建议你创建并打开该文件的副本, 以便不会意外更改任何属性。

1. 仅适用于 2017 SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. 获取**PYTHONHOME**的值。
3. 获取当前工作目录的值。

> [!NOTE]
> 如果你在 SQL Server 2017 中安装了 Python 和 R, 则适用于 R 和 Python 语言的工作目录和工作目录池。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>是否安装了多个 R 或 Python 实例？

查看是否在计算机上安装了 R 库的多个副本。 如果出现以下情况, 则可能发生此重复:

* 在安装过程中, 你可以选择 R Services (数据库内) 和 R Server (独立)。
* 除了 SQL Server 之外, 还可以安装 Microsoft R Client。
* 使用针对 Visual Studio 的 R 工具、R Studio、Microsoft R Client 或其他 R IDE 安装了一组不同的 R 库。
* 计算机承载 SQL Server 的多个实例, 且多个实例使用机器学习。

同样的条件适用于 Python。

如果发现安装了多个库或运行时, 请确保仅获取与 SQL Server 实例使用的 Python 或 R 运行时相关联的错误。

## <a name="origin-of-errors"></a>错误源

尝试运行 R 代码时看到的错误可以来自以下任何源:

* SQL Server 数据库引擎, 包括存储过程 sp_execute_external_script
* SQL Server 受信任的快速启动板
* 扩展性框架的其他组件, 包括 R 和 Python 启动器以及附属进程
* 提供程序, 如 Microsoft 开放式数据库连接 (ODBC)
* R 语言

第一次使用该服务时, 可能很难判断哪些消息来自哪些服务。 建议您不仅捕获准确的消息文本, 而且还捕获消息所用的上下文。 请注意用于运行机器学习代码的客户端软件:

* 是否在使用 Management Studio？ 外部应用程序？
* 您是在远程客户端还是直接在存储过程中运行 R 代码？

## <a name="sql-server-log-files"></a>SQL Server 日志文件

获取最新 SQL Server 错误日志。 完整的一组错误日志包含以下默认日志目录中的文件:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 确切的文件夹名称不同, 具体取决于实例的名称。

## <a name="errors-returned-by-spexecuteexternalscript"></a>Sp_execute_external_script 返回的错误

当你运行 sp_execute_external_script 命令时, 获取返回的完整错误文本 (如果有)。

若要删除 R 或 Python 问题, 你可以运行此脚本, 该脚本将启动 R 或 Python 运行时, 并来回传递数据。

**对于 R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**用于 Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>扩展性框架生成的错误

SQL Server 为外部脚本语言运行时生成单独的日志。 这些错误不是由 Python 或 R 语言生成的。 它们是从 SQL Server 中的扩展性组件生成的, 包括特定于语言的启动器及其附属进程。

可以从以下默认位置获取这些日志:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 确切的文件夹名称与实例名称不同。 根据你的配置, 文件夹可能位于不同的驱动器上。

例如, 以下日志消息与扩展性框架相关:

* *用户 MSSQLSERVER01 的 LogonUser 失败*
  
  这可能表示运行外部脚本的辅助角色帐户无法访问实例。

* *InitializePhysicalUsersPool 失败*
  
  此消息可能表示你的安全设置阻止安装程序创建运行外部脚本所需的工作线程帐户池。

* *安全上下文管理器初始化失败*

* *附属会话管理器初始化失败*

## <a name="system-events"></a>系统事件

1. 打开 Windows 事件查看器, 并在**系统事件**日志中搜索包含字符串*快速启动板*的消息。
2. 打开 ExtLaunchErrorlog 文件, 并查找字符串*错误代码*。 查看与 ErrorCode 关联的消息。

例如, 以下消息是与 SQL Server 扩展性框架相关的常见系统错误:

* *由于以下错误, SQL Server Launchpad (MSSQLSERVER) 服务启动失败:<text>*

* *该服务未及时响应启动请求或控制请求。*

* *等待 SQL Server Launchpad (MSSQLSERVER) 服务连接时达到超时 (120000 毫秒)。*

## <a name="dump-files"></a>转储文件

如果你熟悉调试, 则可以使用转储文件来分析快速启动板中的失败。

1. 找到包含 SQL Server 的安装程序启动日志的文件夹。 例如, 在 SQL Server 2016 中, 默认路径为 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\log 处
2. 打开特定于扩展性的启动日志子文件夹。
3. 如果需要提交支持请求, 请将此文件夹的全部内容添加到压缩文件中。 例如, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
确切位置在您的系统上可能会有所不同, 并且可能位于 C 驱动器以外的驱动器上。 确保获取安装机器学习的实例的日志。

## <a name="configuration-settings"></a>配置设置

本部分列出了运行 R 或 Python 脚本时可能成为错误源的其他组件或提供程序。

### <a name="what-network-protocols-are-available"></a>可用的网络协议是什么？

机器学习服务需要以下网络协议来实现扩展性组件之间的内部通信, 以及与外部 R 或 Python 客户端的通信。

* Named pipes
* TCP/IP

打开 SQL Server 配置管理器确定是否安装了协议, 并确定是否已启用。

### <a name="security-configuration-and-permissions"></a>安全配置和权限

对于辅助角色帐户:

1. 在 "控制面板" 中, 打开 "**用户和组**", 然后找到用于运行外部脚本作业的组。 默认情况下, 组为**SQLRUserGroup**。
2. 验证该组是否存在并且是否包含至少一个辅助角色帐户。
3. 在 SQL Server Management Studio 中, 选择将运行 R 或 Python 作业的实例, 选择 "**安全性**", 然后确定是否存在 SQLRUserGroup 的登录。
4. 查看用户组的权限。

对于单个用户帐户:

1. 确定实例是支持混合模式身份验证、仅限 SQL 登录名还是仅支持 Windows 身份验证。 此设置会影响 R 或 Python 代码要求。
2. 对于需要运行 R 代码的每个用户, 确定要从 R 写入对象的每个数据库的所需权限级别, 将访问数据或创建对象。
3. 若要启用脚本执行, 请根据需要创建角色或将用户添加到下列角色:

   - 除*db_owner*之外的所有内容:需要执行任何外部脚本。
   - *db_datawriter*：写入 R 或 Python 的结果。
   - *db_ddladmin*：创建新的对象。
   - *db_datareader*：读取 R 或 Python 代码所用的数据。
4. 请注意, 在安装 SQL Server 2016 时是否更改了任何默认启动帐户。
5. 如果用户需要安装新的 R 包或使用其他用户安装的 R 包, 则可能需要在实例上启用包管理, 并分配其他权限。 有关详细信息, 请参阅[启用或禁用 R 包管理](r/r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>哪些文件夹受防病毒软件的锁定？

防病毒软件可以锁定文件夹, 这会阻止计算机学习功能的设置和成功执行脚本。 确定 SQL Server 树中的任何文件夹是否受病毒扫描的限制。

但是, 当在一个实例上安装多个服务或功能时, 可能很难枚举该实例使用的所有可能的文件夹。 例如, 在添加新功能时, 必须标识并排除新的文件夹。

此外, 某些功能在运行时动态创建新文件夹。 例如, 内存中 OLTP 表、存储过程和函数都在运行时创建新的目录。 这些文件夹名称通常包含 Guid, 无法预测。 SQL Server 受信任的快速启动板为 R 和 Python 脚本作业创建新的工作目录。

因为可能无法排除 SQL Server 进程及其功能所需的所有文件夹, 所以建议你排除整个 SQL Server 实例目录树。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>防火墙是否为 SQL Server 打开？ 实例是否支持远程连接？

1. 若要确定 SQL Server 是否支持远程连接, 请参阅[配置远程服务器连接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 确定是否已为 SQL Server 创建防火墙规则。 出于安全原因, 在默认安装中, 远程 R 或 Python 客户端可能无法连接到该实例。 有关详细信息, 请参阅[疑难解答连接到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

## <a name="see-also"></a>请参阅

[SQL Server 中的机器学习疑难解答](machine-learning-troubleshooting-faq.md)
