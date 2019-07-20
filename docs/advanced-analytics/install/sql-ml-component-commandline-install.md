---
title: 命令提示符安装 R 和 Python 组件
description: 运行 SQL Server 命令行安装程序, 将 R 语言和 Python 集成添加到 SQL Server 数据库引擎实例。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86f17e9775108e9b075b3733df59202654888d62
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345026"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>从命令行安装 SQL Server 机器学习 R 和 Python 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了安装 SQL Server 机器学习组件的命令行说明:

+ [数据库中的新实例](#indb)
+ [添加到现有数据库引擎实例](#add-existing)
+ [无提示安装](#silent)
+ [新建独立服务器](#shared-feature)

您可以指定与安装程序用户界面的 "无提示"、"基本" 或 "完全" 交互。 本文补充[了从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), 涵盖了 R 和 Python 机器学习组件独有的参数。

## <a name="pre-install-checklist"></a>预安装清单

+ 从提升权限的命令提示符运行命令。 

+ 数据库引擎实例是数据库内安装所必需的。 你不能仅安装 R 或 Python 功能, 但你可以[将它们增量添加到现有实例](#add-existing)。 如果只想要没有数据库引擎的 R 和 Python, 请安装[独立服务器](#shared-feature)。

+ 不要在故障转移群集上安装。 用于隔离 R 和 Python 进程的安全机制与 Windows Server 故障转移群集环境不兼容。

+ 不要在域控制器上安装。 安装程序的机器学习服务部分将失败。

+ 避免在同一台计算机上安装独立和数据库中的实例。 独立服务器将争夺相同的资源，从而损害两种安装的性能。


## <a name="command-line-arguments"></a>命令行参数

功能参数是必需的, 这与许可条款协议相同。 

通过命令提示符安装时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持完全静默模式（通过使用 /Q 参数）或简单静默模式（通过使用 /QS 参数）。 /QS 开关仅显示进度，不接受任何输入，也不显示错误消息（如果遇到）。 仅当指定 /Action=install 时才支持 /QS 参数。

| 参数 | 描述 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 安装数据库内版本:SQL Server 2017 机器学习服务 (数据库内) 或 SQL Server 2016 R Services (数据库内)。  |
| /FEATURES = SQL_INST_MR | 仅适用于 2017 SQL Server。 将此与 AdvancedAnalytics 配对。 安装 (数据库中) R 功能, 包括 Microsoft R Open 和专用的 R 包。 SQL Server 2016 R Services 功能是仅限 R 的, 因此该版本没有参数。|
| /FEATURES = SQL_INST_MPY | 仅适用于 2017 SQL Server。 将此与 AdvancedAnalytics 配对。 安装 (数据库中) Python 功能, 包括 Anaconda 和专有 Python 包。 |
| /FEATURES = SQL_SHARED_MR | 为独立版本安装 R 功能:SQL Server 2017 Machine Learning Server (独立版) 或 SQL Server 2016 R Server (独立版)。 独立服务器是未绑定到数据库引擎实例的 "共享功能"。|
| /FEATURES = SQL_SHARED_MPY | 仅适用于 2017 SQL Server。 为独立版本安装 Python 功能:SQL Server 2017 Machine Learning Server (独立版)。 独立服务器是未绑定到数据库引擎实例的 "共享功能"。|
| /IACCEPTROPENLICENSETERMS  | 指示已接受使用开源 R 组件的许可条款。 |
| /IACCEPTPYTHONLICENSETERMS | 指示已接受使用 Python 组件的许可条款。 |
| /IACCEPTSQLSERVERLICENSETERMS | 指示已接受使用 SQL Server 的许可条款。|
| /MRCACHEDIRECTORY | 对于脱机安装程序, 设置包含 R 组件 CAB 文件的文件夹。 |
| /MPYCACHEDIRECTORY | 保留供将来使用。 使用% TEMP% 可在没有 internet 连接的计算机上存储 Python 组件 CAB 文件以供安装。 |


## <a name="indb"></a>数据库内实例安装

数据库内分析可用于数据库引擎实例, 这是将**AdvancedAnalytics**功能添加到安装所必需的。 您可以使用高级分析安装数据库引擎实例, 或[将其添加到现有实例](#add-existing)。 

若要查看进度信息而不显示交互式屏幕提示, 请使用/qs 参数。

> [!IMPORTANT]
> 安装完成后, 将保留两个额外的配置步骤。 执行这些任务之前, 不会完成集成。 有关说明, 请参阅[安装后任务](#post-install)。

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: 数据库引擎、具有 Python 和 R 的高级分析

对于数据库引擎实例的并发安装, 请提供实例名称和管理员 (Windows) 登录名。 包括用于安装核心和语言组件的功能, 以及对所有许可条款的接受。

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

这是相同的命令, 但在使用混合身份验证的数据库引擎上使用 SQL Server 登录名。

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此示例仅为 Python, 显示你可以通过省略功能添加一种语言。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: 与 R 的数据库引擎和高级分析

此命令与 SQL Server 2017 完全相同, 但没有 Python 元素, 这些元素在 SQL Server 2016 安装程序中不可用。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a>安装后配置 (必需)

仅适用于数据库中安装。

安装完成后, 你将拥有一个具有 R 和 Python 的数据库引擎实例、Microsoft R 和 Python 包、Microsoft R Open、Anaconda、工具、示例以及作为分发的一部分的脚本。 

要完成安装, 需要执行两个任务:

1. 重新启动数据库引擎服务。

1. 启用外部脚本, 然后才能使用该功能。 按照[安装 SQL Server 2017 机器学习服务 (数据库内)](sql-machine-learning-services-windows-install.md)中的说明进行下一步。 

对于 SQL Server 2016, 请改用本文[SQL Server 2016 R Services (数据库内)](sql-r-services-windows-install.md)。

## <a name="add-existing"></a>向现有数据库引擎实例添加高级分析

向现有数据库引擎实例添加数据库中高级分析时, 请提供实例名称。 例如, 如果之前安装了 SQL Server 2017 数据库引擎和 Python, 则可以使用此命令添加 R。

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a>无提示安装

无提示安装会禁止检查 .cab 文件位置。 出于此原因, 必须指定要解压缩 .cab 文件的位置。 对于 Python, CAB 文件必须位于% TEMP * 中。 对于 R, 可以使用来设置文件夹路径。
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a>独立服务器安装

独立服务器是未绑定到数据库引擎实例的 "共享功能"。 下面的示例显示了这两个版本的有效语法。

SQL Server 2017 支持在独立服务器上使用 Python 和 R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 仅限 R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

安装完成后, 你将拥有服务器、Microsoft 包、R 和 Python 的开源分发版、工具、示例以及作为分发的一部分的脚本。 

若要打开 R 控制台窗口, 请参阅 \Program files\Microsoft SQL Server\140 (或 130) \R_SERVER\bin\x64, 然后双击 " **rgui.exe**"。 不熟悉 R？ 尝试学习本教程:[基本 R 命令和 RevoScaleR 函数:25个常见](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)示例。

若要打开 Python 命令, 请参阅 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\bin\x64, 然后双击 " **python**"。

## <a name="get-help"></a>获取帮助

安装或升级需要帮助？ 有关常见问题的解答, 请参阅以下文章:

* [升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并解决常见问题, 请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例, 并了解 R 如何与 SQL Server 相关的基础知识。 下一步, 请参阅以下链接:

+ [教程：在 T-sql 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教程：适用于 R 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 配合使用:

+ [教程：在 T-sql 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [教程：适用于 Python 开发人员的数据库内分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于实际场景的机器学习示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。