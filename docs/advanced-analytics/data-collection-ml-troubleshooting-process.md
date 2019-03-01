---
title: 机器学习-SQL Server 机器学习服务的数据集合疑难解答
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: edfacb2e4d519d4f709d352f52645526cb341fad
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017933"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>机器学习的数据集合疑难解答

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了你尝试时应使用来解决自己的问题或帮助 Microsoft 客户支持的数据收集方法。

**适用范围：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务 （R 和 Python）

## <a name="sql-server-version-and-edition"></a>SQL Server 版本和版本类别

SQL Server 2016 R Services 是 SQL Server 包含 R 的集成的支持的第一个版本。 SQL Server 2016 Service Pack 1 (SP1) 包含几个主要的改进，包括运行外部脚本的能力。 如果你是 SQL Server 2016 客户，则应考虑安装 SP1 或更高版本。

SQL Server 2017 添加 Python 语言集成。 在早期版本中，无法获取 Python 功能集成。

有关帮助获取版本和版本，请参阅本文中，这将为每个列出的内部版本号[SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)。

具体取决于正在使用的 SQL Server 版本，某些机器学习功能可能不可用，或限制。 以下文章列表上的 Enterprise、 Developer、 Standard 和 Express 版本中的机器学习功能。

* [版本和支持的 SQL Server 功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R 和 Python 版本的 SQL Server 的功能](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 语言和工具版本

一般情况下，选择 R Services 功能或机器学习服务功能时安装的 Microsoft R 的版本确定通过 SQL Server 内部版本号。 如果您升级或修补 SQL Server，还必须升级或修补程序及其 R 组件。

有关发布和下载 R 组件的链接的列表，请参阅[安装没有 internet 访问权限的机器学习组件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在具有 internet 访问的计算机，所需的 R 版本是标识，并自动安装。

就可以单独从称为绑定的过程中的 SQL Server 数据库引擎升级 R Server 组件。 因此，具体取决于安装的 SQL Server 版本以及是否具有服务器迁移到最新的 R 版本可能与不同的 SQL Server 中运行 R 代码时使用的 R 版本。

### <a name="determine-the-r-version"></a>确定 R 版本

若要确定 R 版本的最简单方法是通过运行如下所示的语句获取的运行时属性：

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
> 如果不使用 R Services，请尝试从 RGui 运行 R 脚本部分。

作为最后的手段，您可以打开要确定安装的版本的服务器上的文件。 若要执行此操作，找到 rlauncher.config 文件，以获取 R 运行时和当前工作目录的位置。 我们建议您创建并打开文件的副本，以便不会意外更改的任何属性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要获取的 R 版本和 RevoScaleR 版本，请打开 R 命令提示符，或打开 RGui 与实例相关联。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

在 R 控制台在启动时显示的版本信息。 例如，以下版本表示 SQL Server 2017 的默认配置：

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 版本

有几种方法可获取 Python 版本。 最简单方法是从 Management Studio 或任何其他 SQL 查询工具运行此语句：

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

如果未运行机器学习服务，可以通过查看 pythonlauncher.config 文件来确定已安装的 Python 版本。 我们建议您创建并打开文件的副本，以便不会意外更改的任何属性。

1. 对于 SQL Server 2017 仅： `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. 获取的值**PYTHONHOME**。
3. 获取当前工作目录的值。

> [!NOTE]
> 如果已在 SQL Server 2017 中安装 Python 和 R，工作目录和辅助角色帐户的池共享的 R 和 Python 语言。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>多个实例的 R 或 Python 安装？

检查是否在计算机上安装的 R 库的多个副本。 如果，则可能发生这种重复：

* 在安装期间选择 R Services （数据库内） 和 R Server （独立版）。
* 安装 Microsoft R Client 除了 SQL Server。
* Visual Studio、 R Studio、 Microsoft R 客户端，或另一个 R IDE 中使用的 R 工具安装一组不同的 R 库。
* 计算机托管了多个 SQL Server 实例和多个实例使用机器学习。

此规则也适用于 Python。

如果您发现安装了多个库或运行时，请确保您获得仅与 SQL Server 实例使用的 Python 或 R 运行时关联的错误。

## <a name="origin-of-errors"></a>错误的来源

当您尝试运行 R 代码时遇到的错误可能来自任何以下源：

* SQL Server 数据库引擎，包括存储的过程 sp_execute_external_script
* SQL Server 受信任的快速启动板
* 其他组件的可扩展性框架，包括 R 和 Python 启动器和附属进程
* 提供程序，如 Microsoft 开放式数据库连接 (ODBC)
* R 语言

与第一次服务时，将很难判断哪些消息来源于哪些服务。 我们建议您捕获确切的消息文本中，不仅在其中看到消息的上下文。 请注意你要用于运行机器学习代码的客户端软件：

* 使用 Management Studio？ 外部应用程序？
* 在远程客户端，或直接在存储过程是否正在运行 R 代码？

## <a name="sql-server-log-files"></a>SQL Server 日志文件

获取最新的 SQL Server 错误日志。 错误日志的完整集包括的以下默认日志目录中的文件：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 确切的文件夹名称而异的实例名称。

## <a name="errors-returned-by-spexecuteexternalscript"></a>返回 sp_execute_external_script 的错误

运行 sp_execute_external_script 命令时，如果有，获取，返回的错误的完整文本。

若要排除在考虑之外的 R 或 Python 的问题，可以运行此脚本，它启动 R 或 Python 运行时并来回传递数据。

**适用于 R**

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

## <a name="errors-generated-by-the-extensibility-framework"></a>可扩展性框架所生成的错误

SQL Server 生成单独的外部脚本语言运行时的日志。 这些错误不由 Python 或 R 语言生成。 生成时将其从 SQL Server，包括特定于语言的启动器和其附属进程中的可扩展性组件。

可以从以下默认位置获取这些日志：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE]
> 根据实例名称的确切的文件夹名称有所不同。 具体取决于您的配置，该文件夹可能是不同的驱动器上。

例如，与可扩展性框架相关的以下日志消息：

* *用户 MSSQLSERVER01 LogonUser 失败*
  
  这可能表示运行外部脚本的辅助角色帐户无法访问实例。

* *InitializePhysicalUsersPool 失败*
  
  此消息可能意味着您的安全设置将阻止安装程序创建辅助角色帐户来运行外部脚本所需的池。

* *安全上下文管理器初始化失败*

* *附属会话管理器初始化失败*

## <a name="system-events"></a>系统事件

1. 打开 Windows 事件查看器，并搜索**系统事件**日志中是否包含字符串的消息*快速启动板*。
2. 打开 ExtLaunchErrorlog 文件，并查找字符串*ErrorCode*。 查看与错误代码关联的消息。

例如，下面的消息是与 SQL Server 可扩展性框架相关的常见系统错误：

* *SQL Server 快速启动板 (MSSQLSERVER) 服务启动因以下错误而失败：  <text>*

* *该服务未响应及时的开始或控制请求。*

* *等待要连接的 SQL Server 快速启动板 (MSSQLSERVER) 服务时达到超时时间 （120000 毫秒为单位）。*

## <a name="dump-files"></a>转储文件

如果您非常了解调试，可以使用转储文件来分析快速启动板中的失败。

1. 找到包含 SQL Server 安装程序启动日志的文件夹。 例如，在 SQL Server 2016 中，默认路径为 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log。
2. 打开特定于可扩展性的 bootstrap 日志子文件夹。
3. 如果你需要提交支持请求，将此文件夹的全部内容添加到一个压缩文件。 例如，C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
确切位置上您的系统，可能会有所不同，它可能是 C 驱动器以外的驱动器上。 请务必安装机器学习的实例获取的日志。

## <a name="configuration-settings"></a>配置设置

本部分列出了其他组件或在运行 R 或 Python 脚本时，可以是错误的源的提供程序。

### <a name="what-network-protocols-are-available"></a>提供了哪些网络协议？

机器学习服务需要以下网络协议的可扩展性组件之间的内部通信和与外部 R 或 Python 客户端进行通信。

* Named pipes
* TCP/IP

打开 SQL Server 配置管理器来确定是否安装了一种协议，如果已安装，以确定是否启用。

### <a name="security-configuration-and-permissions"></a>安全配置和权限

对于辅助角色帐户：

1. 在控制面板中，打开**用户和组**，并找到用于运行外部脚本作业的组。 默认情况下，组是**SQLRUserGroup**。
2. 验证的组存在，并且包含至少一个辅助角色帐户。
3. 在 SQL Server Management Studio 中，选择的实例，其中将运行 R 或 Python 的作业，选择**安全**，然后再来决定是否存在 SQLRUserGroup 的登录。
4. 查看用户组的权限。

为单个用户帐户：

1. 确定实例是否支持混合模式身份验证、 SQL 登录名或仅使用 Windows 身份验证。 此设置会影响你的 R 或 Python 代码的要求。
2. 对于每个用户都需要运行 R 代码，确定所需的每个数据库，将从 R 编写对象、 将访问数据，或将创建对象的权限级别。
3. 若要启用脚本执行，请创建角色，或将用户添加到以下角色中，根据需要：

   - 以外的所有*db_owner*:需要执行任何外部脚本。
   - *db_datawriter*：若要从 R 或 Python 写入结果。
   - *db_ddladmin*：若要创建新对象。
   - *db_datareader*：若要读取 R 或 Python 代码使用的数据。
4. 请注意当你安装 SQL Server 2016 时是否更改任何默认的启动帐户。
5. 如果用户需要安装新的 R 包或使用其他用户已安装的 R 包，您可能需要在实例上启用包管理并分配其他权限。 有关详细信息，请参阅[启用或禁用 R 包管理](r/r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>锁定的防病毒软件受到哪些文件夹？

防病毒软件可以锁定的文件夹，从而阻止这两个安装程序的机器学习功能和成功的脚本执行。 确定 SQL Server 树中的任何文件夹是否受到病毒扫描。

但是，当实例上安装了多个服务或功能，它可能很难枚举的实例使用的所有可能的文件夹。 例如，添加新功能，必须标识新的文件夹，并排除。

此外，某些功能的新文件夹动态创建在运行时。 例如，内存中 OLTP 表、 存储的过程和函数所有在运行时创建新目录。 通常，这些文件夹名称包含 Guid，并且无法预测。 SQL Server Trusted Launchpad 创建新的工作目录为 R 和 Python 脚本的作业。

因为它可能不是可以排除所需的 SQL Server 进程和及其功能的所有文件夹，我们建议你都排除整个 SQL Server 实例目录树。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>是 SQL Server 防火墙打开？ 该实例是否支持远程连接？

1. 若要确定 SQL Server 是否支持远程连接，请参阅[配置远程服务器连接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 确定是否已为 SQL Server 创建防火墙规则。 出于安全原因，在默认安装中，它可能无法远程 R 或 Python 客户端来连接到的实例。 有关详细信息，请参阅[故障排除连接到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

## <a name="see-also"></a>另请参阅

[对 SQL Server 中的机器学习进行故障排除](machine-learning-troubleshooting-faq.md)
