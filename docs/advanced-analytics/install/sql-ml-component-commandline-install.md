---
title: 命令提示符下安装 R 和 Python 组件的 SQL Server 机器学习
description: 运行 SQL Server 命令行安装程序将 R 语言和 Python 集成添加到 SQL Server 数据库引擎实例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ffd4b13d5ab92187ac998fd983e8fa8416e4401
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962896"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>安装 SQL Server 机器学习命令行中的 R 和 Python 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了有关安装 SQL Server 机器学习命令行中的组件的说明：

+ [新的在数据库实例](#indb)
+ [将添加到现有的数据库引擎实例](#add-existing)
+ [无提示安装](#silent)
+ [新的独立服务器](#shared-feature)

您可以指定与安装程序用户界面的无提示、 基本或完全交互。 本文补充[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，涵盖唯一的 R 和 Python 机器学习组件的参数。

## <a name="pre-install-checklist"></a>预安装清单

+ 从提升的命令提示符运行的命令。 

+ 需要在数据库中安装数据库引擎实例。 不能安装只是 R 或 Python 功能，尽管你可以[以增量方式将它们添加到现有实例](#add-existing)。 如果您希望只是 R 和 Python 不带数据库引擎，安装[独立服务器](#shared-feature)。

+ 在故障转移群集上未安装。 用于隔离 R 和 Python 进程的安全机制不兼容与 Windows Server 故障转移群集环境。

+ 不要在域控制器上安装。 安装程序的机器学习服务部分将会失败。

+ 避免在同一台计算机上安装独立应用程序和数据库实例。 独立服务器将争夺相同的资源，从而损害两种安装的性能。


## <a name="command-line-arguments"></a>命令行参数

功能参数是必需的因为许可条款协议。 

通过命令提示符安装时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持完全静默模式（通过使用 /Q 参数）或简单静默模式（通过使用 /QS 参数）。 /QS 开关仅显示进度，不接受任何输入，也不显示错误消息（如果遇到）。 仅当指定 /Action=install 时才支持 /QS 参数。

| 参数 | 描述 |
|-----------|-------------|
| / 功能 = AdvancedAnalytics | 安装中数据库版本：SQL Server 2017 机器学习服务 （数据库内） 或 SQL Server 2016 R Services （数据库内）。  |
| /FEATURES = SQL_INST_MR | 适用于仅 SQL Server 2017。 与 AdvancedAnalytics 配对这。 安装 （数据库内） R 功能，包括 Microsoft R Open 和专有 R 包。 SQL Server 2016 R Services 功能是 R 仅，因此没有适用于版参数。|
| /FEATURES = SQL_INST_MPY | 适用于仅 SQL Server 2017。 与 AdvancedAnalytics 配对这。 安装的 Python （数据库内） 功能，包括 Anaconda 和专有的 Python 包。 |
| /FEATURES = SQL_SHARED_MR | 安装独立版本的 R 功能：SQL Server 2017 机器学习服务器 （独立版） 或 SQL Server 2016 R Server （独立版）。 独立服务器是未绑定到数据库引擎实例的"共享的功能"。|
| /FEATURES = SQL_SHARED_MPY | 适用于仅 SQL Server 2017。 安装独立版本的 Python 功能：SQL Server 2017 机器学习服务器 （独立版）。 独立服务器是未绑定到数据库引擎实例的"共享的功能"。|
| /IACCEPTROPENLICENSETERMS  | 指示已接受使用开放源代码 R 组件的许可条款。 |
| /IACCEPTPYTHONLICENSETERMS | 指示已接受使用 Python 组件的许可条款。 |
| /IACCEPTSQLSERVERLICENSETERMS | 指示已接受有关使用 SQL Server 的许可条款。|
| /MRCACHEDIRECTORY | 脱机安装程序将设置包含 R 组件 CAB 文件的文件夹。 |
| / MPYCACHEDIRECTORY | 保留供将来使用。 使用 %TEMP%存储不具有 internet 连接的计算机上安装的 Python 组件 CAB 文件。 |


## <a name="indb"></a> 数据库实例安装

数据库内分析是可供数据库引擎实例，添加所需**AdvancedAnalytics**到你的安装的功能。 您可以使用高级分析功能，安装数据库引擎实例或[将其添加到现有实例](#add-existing)。 

若要查看进度信息而无需交互式屏幕提示，请使用 /qs 参数。

> [!IMPORTANT]
> 安装完成后，保持两个额外的配置步骤。 直到执行这些任务，才会完成集成。 请参阅[安装后任务](#post-install)有关的说明。

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017： 数据库引擎、 高级分析，包括 Python 和 R

对于数据库引擎实例的并行安装，提供实例名称和管理员 (Windows) 登录名。 包括用于安装核心和语言组件，以及所有许可条款的接受的功能。

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此相同的命令，但在数据库引擎使用的 SQL Server 登录名具有混合身份验证。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此示例显示，您可以通过省略一项功能添加一种语言，是 Python。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016： 数据库引擎和高级的分析使用 R

此命令等同于 SQL Server 2017，但不包含 Python 元素，其中中均不提供 SQL Server 2016 安装程序。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 安装后配置 （必需）

适用于数据库中仅安装。

安装程序完成后，可以使用 R 和 Python、 Microsoft R 和 Python 包、 Microsoft R Open，Anaconda、 工具、 示例和脚本的一部分分发的数据库引擎实例。 

完成安装需要两个更多的任务：

1. 重新启动数据库引擎服务。

1. 启用外部脚本，然后才能使用该功能。 按照中的说明[安装 SQL Server 2017 机器学习服务 （数据库内）](sql-machine-learning-services-windows-install.md)作为下一步。 

对于 SQL Server 2016 中，使用本文相反[安装 SQL Server 2016 R Services （数据库内）](sql-r-services-windows-install.md)。

## <a name="add-existing"></a> 将高级分析功能添加到现有的数据库引擎实例

当将数据库内高级分析功能添加到现有的数据库引擎实例，提供实例名称。 例如，如果您以前安装了 SQL Server 2017 数据库引擎和 Python，您可以使用此命令将添加。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 无提示安装

无提示安装取消.cab 文件位置的检查。 出于此原因，必须指定.cab 文件的位置进行解包的位置。 对于 Python，CAB 文件必须位于 %temp *。 对于 R，可以设置文件夹路径使用您为此可以临时目录。
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> 独立服务器安装

独立服务器是未绑定到数据库引擎实例的"共享的功能"。 以下示例演示这两个版本的有效语法。

SQL Server 2017 支持在独立服务器上的 Python 和 R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 的仅限 R 的：

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

安装程序完成后，必须在服务器、 Microsoft 包、 开放源代码的 R 和 Python，工具、 示例和脚本的一部分分发的分发版。 

若要打开 R 控制台窗口中，转到 \Program files\Microsoft SQL Server\140 （或 130） \R_SERVER\bin\x64，然后双击**RGui.exe**。 不熟悉 R？ 请尝试本教程中：[基本 R 命令和 RevoScaleR 函数：25 的常见示例](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)。

若要打开 Python 命令，转到 files\microsoft SQL Server\140\PYTHON_SERVER\bin\x64，并双击**python.exe**。

## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查的实例的安装状态并解决常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程：R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 与 SQL Server 使用按照这些教程：

+ [教程：在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [教程：面向 Python 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于实际场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。