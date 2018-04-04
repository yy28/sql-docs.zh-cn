---
title: 解决 SQL Server 的用于机器学习的数据收集
ms.custom: ''
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bb4c8d097cd548ad256f84d513e597e934873e69
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>解决机器学习的数据收集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文讨论尝试解决安装程序、 配置或 SQL Server 中的机器学习的性能问题时，应收集的数据的类型。 此类数据包括日志、 错误消息和系统信息。

本文介绍的是最有用的信息来源时执行的自助基础的诊断。 收集此信息也是有用时请求与 SQL Server 机器学习功能相关的问题的技术支持。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （R 和 Python）

## <a name="sql-server-and-r-versions"></a>SQL Server 和 R 版本

请注意版本为新安装或升级。 如果是升级，确定执行的方式：

- 你未从升级哪个版本？ 
- 你未删除旧的组件，或未就地升级？
- 你未在升级过程中更改了任何功能选项？ 

### <a name="which-edition-of-sql-server-is-installed-and-which-version"></a>安装了 SQL Server 的版本和哪个版本？ 

SQL Server 2016 中引入了 SQL Server R Services。 以前的版本不支持机器学习。 此外，后续的 service pack 2016 版本包含许多 bug 修复和改进。 第一步，你应考虑安装 Service Pack 1 或更高版本。

在 SQL Server 自 2017 年，支持将扩展到 Python 语言。 在早期版本中未提供对 Python 的支持。

如果你需要帮助确定你拥有的哪些版本和版本，请参阅本文中，其中的每个列出的内部版本号[SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)。

根据你正在使用的 SQL Server 的版本，某些机器学习功能可能不可用，或限制。

请参阅企业、 开发人员、 标准和 Express 版本中的机器学习功能的列表的以下文章。

* [版本和 SQL Server 支持的功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [在 R 功能的 SQL Server 的版本之间的差异](https://docs.microsoft.com/sql/advanced-analytics/r/differences-in-r-features-between-editions-of-sql-server)

### <a name="which-version-of-microsoft-r-is-installed"></a>安装 Microsoft R 哪个版本？

通常情况下，当你选择了 R 服务功能或机器学习服务功能安装的 Microsoft R 的版本确定通过 SQL Server 内部版本号。 如果升级或修补程序的 SQL Server 时，还必须升级或修补程序及其 R 组件。

有关版本和 R 组件下载链接列表，请参阅[安装没有 internet 访问权限的机器学习组件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在计算机上具有 internet 访问权限，所需的 R 版本是标识，并自动安装。

可从该过程称为绑定中的 SQL Server 数据库引擎的单独升级 R Server 组件。 因此，具体取决于安装的 SQL Server 版本和是否具有服务器迁移到最新的 R 版本可能会与不同的 SQL Server 中运行 R 代码时所用的 R 版本。

#### <a name="determine-the-r-version"></a>确定 R 版本

若要确定 R 版本的最简单方法是通过运行如下所示语句来获取运行时属性：

```SQL
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
> 如果 R Services 未工作，请尝试从 RGui 运行 R 的脚本部分。

作为最后一招，您可以打开要确定安装的版本的服务器上的文件。 为此，请找到 rlauncher.config 文件，以获取 R 运行时和当前工作目录的位置。 我们建议您创建并打开文件的副本，以便不会意外更改任何属性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要获取的 R 版本和 RevoScaleR 版本，请打开 R 命令提示符，或打开 RGui 与实例相关联。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`


R 控制台在启动时显示的版本信息。 例如，以下版本表示 SQL Server 自 2017 年 1 CTP 2.0 的默认配置：

    *Microsoft R Open 3.3.3*
    
    *The enhanced R distribution from Microsoft*
    
    *Microsoft packages Copyright (C) 2017 Microsoft*
    
    *Loading Microsoft R Server packages, version 9.1.0.*


### <a name="what-version-of-python-is-installed"></a>安装哪个版本的 Python？

仅在 SQL Server 自 2017 年 1 社区技术预览版 (CTP) 2.0 和更高版本，支持 Python 的。

有多种方法可获取的 Python 版本。 最简单方法是从 Management Studio 或任何其他 SQL 查询工具运行此语句：

```SQL
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

如果机器学习服务未运行，则可以通过查看 pythonlauncher.config 文件来确定已安装的 Python 版本。 我们建议您创建并打开文件的副本，以便不会意外更改任何属性。

1. 对于 SQL Server 自 2017 年 1 仅： `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. 获取的值**PYTHONHOME**。
3. 获取当前工作目录的值。


> [!NOTE]
> 如果你已在 SQL Server 2017 安装 Python 和 R，工作目录和工作人员帐户的库共享 R 和 Python 语言。

### <a name="are-multiple-instances-of-r-or-python-installed"></a>R 的多个实例或 Python 已安装？

检查以确定是否在计算机上安装的 R 库的多个副本。 如果可能发生这种重复：

* 在安装期间选择 R Services （数据库） 和 R Server （独立）。 
* 安装 Microsoft R 除了 SQL Server 的客户端。
* 一组不同的 R 库已通过使用适用于 Visual Studio、 R Studio、 Microsoft R 客户端或另一个的 R IDE R 工具安装。
* 计算机托管了多个 SQL Server 实例和多个实例使用机器学习。

此规则也适用于 Python。

如果你找到安装的多个库或运行时，请确保你获取仅由 SQL Server 实例使用的 Python 或 R 运行时与关联的错误。

## <a name="errors-and-messages"></a>错误和消息

你尝试运行 R 代码时看到的错误可能来自于任何以下源：

- SQL Server 数据库引擎，包括存储的过程 sp_execute_external_script
- SQL Server 受信任的快速启动板 
- 扩展性框架，包括 R 和 Python 启动器和附属进程的其他组件
- 提供程序，如 Microsoft 打开数据库连接 (ODBC)
- R 语言

当使用第一次的服务时，它可能很难判断哪些消息来源于哪些服务。 我们建议你捕获确切的消息文本中，不仅能在其中你将看到消息的上下文。 请注意你要用于运行机器学习代码的客户端软件：

- 你是否正在使用 Management Studio？ 外部应用程序？
- 在远程客户端，或直接在存储过程中，你将运行 R 代码？

### <a name="what-errors-has-sql-server-logged"></a>SQL Server 已记录哪些错误？

获取最新的 SQL Server 错误日志。 错误日志的完整集包含以下默认日志目录中的文件：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE] 
> 确切的文件夹名称取决于实例名称。


### <a name="what-errors-were-returned-by-the-spexecuteexternalscript-command"></a>Sp_execute_external_script 命令返回了哪些错误？

如果有的话，在运行 sp_execute_external_script 命令，就会将返回的错误的完整文本。 

要将 R 或 Python 问题在考虑之外，你可以运行此脚本，它启动 R 或 Python 运行时并来回传递数据。

**R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**For Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

### <a name="what-errors-are-generated-by-the-extensibility-framework"></a>由扩展性框架生成什么错误？

SQL Server 生成单独的外部脚本语言运行时日志。 这些错误不由 Python 或 R 语言生成。 从 SQL Server，包括特定于语言的启动器和其附属进程中的可扩展性组件生成它们时。

你可以从以下默认位置获取这些日志：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE] 
> 确切的文件夹名称因不同而异的实例名称。 根据您配置，该文件夹可能是不同的驱动器上。

例如，下面的日志消息的 extensibility framework 与相关：

* *用户 MSSQLSERVER01 LogonUser 失败*
  
  这可能表示运行外部脚本的工作帐户无法访问的实例。

* *InitializePhysicalUsersPool 失败* 
  
  此消息可能表示你的安全设置，使安装程序，无法创建运行外部脚本所需的工作人员帐户的池。

* *安全上下文管理器初始化失败* 

* *附属会话管理器初始化失败*

### <a name="are-there-any-related-system-events"></a>是否有任何相关的系统事件？

1. 打开 Windows 事件查看器，并搜索**系统事件**日志中是否包含字符串的消息*快速启动板*。 
2. 打开 ExtLaunchErrorlog 文件，并查找字符串*ErrorCode*。 查看与错误代码关联的消息。

例如，下面的消息是与 SQL Server 扩展性框架相关的常见系统错误： 

* *SQL Server 快速启动板 (MSSQLSERVER) 服务启动因以下错误而失败：  <text>*

* *服务未响应及时启动或控制请求。* 

* *等待要连接的 SQL Server 快速启动板 (MSSQLSERVER) 服务时达到超时时间 （120000 毫秒为单位）。* 

### <a name="did-any-components-start-and-then-crash"></a>没有任何组件启动，然后崩溃？

如果要调试的认识，可以使用转储文件来分析快速启动板中的失败。

1. 找到包含 SQL Server 安装程序启动日志的文件夹。 例如，SQL Server 2016 中的默认路径是 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log。
2. 打开特定于扩展性的 bootstrap 日志子文件夹。
3. 如果你需要提交支持请求，请将此文件夹的全部内容添加到压缩文件。 例如，C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
确切的位置可能会与不同在系统上，并且它可能以外 C 驱动器的驱动器上。 请务必安装机器学习的实例中获取的日志。 


## <a name="related-tools-and-configuration"></a>相关的工具和配置

本部分列出了其他组件或运行 R 或 Python 脚本时，可以是错误的源的提供程序。

### <a name="what-network-protocols-are-available"></a>提供了哪些网络协议？

机器学习服务需要以下网络协议，对于扩展性组件间的内部通信和与外部 R 或 Python 客户端通信。

* Named pipes
* TCP/IP

打开 SQL Server 配置管理器以确定是否安装了一种协议，如果已安装，以确定是否启用。

### <a name="security-configuration-and-permissions"></a>安全配置和权限

辅助帐户：

1. 在 Control Panel 中，打开**用户和组**，并找到用于运行外部脚本作业组。 默认情况下，组是**SQLRUserGroup**。
2. 验证的组存在，并且它包含至少一个辅助进程帐户。
3. 在 SQL Server Management Studio，选择的实例 R 或 Python 作业要运行中，选择**安全**，然后确定是否存在 SQLRUserGroup 一个登录名。
4. 查看用户组的权限。

单个用户帐户：

1. 确定实例是否支持混合模式身份验证、 仅限，SQL 登录或 Windows 身份验证。 此设置会影响您的 R 或 Python 代码要求。
2. 每个用户都需要运行 R 代码，确定所需的每个数据库，其中将从 R 编写对象、 将访问数据，或将创建对象的权限级别。
3. 若要启用脚本执行，创建角色，或将用户添加到下列角色，根据需要：

   - 以外的所有*db_owner*： 需要执行任意外部脚本。
   - *db_datawriter*： 若要从 R 或 Python 写入结果。 
   - *db_ddladmin*： 若要创建新对象。 
   - *db_datareader*： 读取使用 R 或 Python 代码的数据。 
4. 请注意是否在安装 SQL Server 2016 时更改了任何默认的启动帐户。
5. 如果用户需要安装新的 R 包，或者使用其他用户已安装的 R 包，你可能需要启用的实例上的管理包，然后分配其他权限。 有关详细信息，请参阅[启用或禁用 R 包管理](r\r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>防病毒软件锁定受到哪些文件夹？

防病毒软件可以锁定文件夹，这将阻止这两个安装程序的机器学习功能和成功的脚本执行。 确定 SQL Server 树中的任何文件夹是否受到病毒扫描。

但是，多个服务或功能安装在实例上，它可能很难枚举的实例使用的所有可能的文件夹。 例如，如果添加新功能，必须标识新的文件夹，并且排除。

此外，某些功能创建新文件夹动态在运行时。 例如，内存中 OLTP 表、 存储的过程和函数所有在运行时创建新目录。 通常，这些文件夹名称包含的 Guid，并且无法预测。 SQL Server 受信任的启动板为 R 创建新的工作目录和 Python 作业编写脚本。

由于它可能不能排除所需的 SQL Server 进程和其功能的所有文件夹，我们建议你都排除整个 SQL Server 实例目录树。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>是 SQL Server 的打开防火墙？ 实例是否支持远程连接？

1. 若要确定 SQL Server 是否支持远程连接，请参阅[配置远程服务器连接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 确定是否已为 SQL Server 创建防火墙规则。 出于安全原因，在默认安装中，它可能无法远程 R 或 Python 的客户端才能连接到的实例。 有关详细信息，请参阅[故障排除连接到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

### <a name="can-you-run-r-script-outside-t-sql"></a>你可以运行 T-SQL 的外部的 R 脚本？

你可以尝试运行 R 运行时通过使用其他 R 工具与 SQL Server 实例关联。 这样一来，你可以确定是否安装了所需的库。

基础安装的 R 包括可用于运行 R 脚本从命令行中，以及 RGui 交互式执行脚本的多个工具。

如果 R 运行时正常工作，但你的脚本返回错误，我们建议你尝试在专用的 R 开发环境，如 R Tools for Visual Studio 中的脚本调试。

我们还建议你查看并略有重写脚本，以更正任何问题与 R 和数据库引擎之间移动数据时，可能会出现的数据类型。 有关详细信息，请参阅[R 库和数据类型](r/r-libraries-and-data-types.md)。

此外，你可以使用 sqlrutils 包将 R 脚本捆绑中的存储过程的过程更轻松地使用的格式。 有关详细信息，请参阅：
* [通过使用 sqlrutils 包生成的 R 代码的存储的过程](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [通过使用 sqlrutils 创建存储的过程](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="see-also"></a>另请参阅

[解决 SQL Server 中的机器学习](machine-learning-troubleshooting-faq.md)
