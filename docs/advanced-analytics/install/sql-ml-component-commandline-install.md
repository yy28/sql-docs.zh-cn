---
title: 命令提示符安装 SQL Server 计算机学习组件 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 921bdddf6ae1638ae637df58a0a7e8301fd91dc0
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>从命令行安装 SQL Server 计算机学习组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供有关安装 SQL Server 机器学习组件从命令行说明：

+ [在数据库实例](#indb)
+ [将添加到现有的数据库引擎实例](#add-existing)
+ [无提示安装](#silent)
+ [独立服务器](#shared-feature)

你可以指定与安装程序用户界面的无提示、 基本，或完全交互。 这篇文章补充[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)，涵盖特有 R 和 Python 机学习组件的参数。

## <a name="pre-install-checklist"></a>预安装清单

+ 从提升的命令提示符处运行的命令。 

+ 数据库引擎实例是必需的数据库中安装。 虽然可以但不能安装只是 R 或 Python 功能，[以增量方式将它们添加到现有实例](#add-existing)。 如果你想仅 R 和 Python 不数据库引擎的情况下，安装[独立服务器](#shared-feature)。

+ 在故障转移群集上未安装。 隔离 R 和 Python 的进程使用的安全机制不与 Windows Server 故障转移群集环境兼容。

+ 不要在域控制器上安装。 安装程序的机器学习服务部分将会失败。

+ 避免在同一台计算机上安装独立应用程序和数据库中实例。 独立服务器会争用同一资源，从而损坏这两个安装的性能。


## <a name="command-line-arguments"></a>命令行参数

功能参数是必需的如将许可条款协议。 

通过命令提示符安装时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持完全静默模式（通过使用 /Q 参数）或简单静默模式（通过使用 /QS 参数）。 /QS 开关仅显示进度，不接受任何输入，也不显示错误消息（如果遇到）。 仅当指定 /Action=install 时才支持 /QS 参数。

| 参数 | Description |
|-----------|-------------|
| / 功能 = AdvancedAnalytics | 安装中数据库版本： SQL Server 自 2017 年 1 机器学习 Services （数据库） 或 SQL Server 2016 R Services （数据库）。  |
| / 功能 = SQL_INST_MR | 适用于仅 SQL Server 自 2017 年。 与 AdvancedAnalytics 配对。 安装 （数据库中） R 功能，包括 Microsoft R Open 和专有的 R 包。 SQL Server 2016 R Services 功能是 R 只读，因此没有该版本参数。|
| / 功能 = SQL_INST_MPY | 适用于仅 SQL Server 自 2017 年。 与 AdvancedAnalytics 配对。 安装 （数据库） Python 功能，包括 Anaconda 和专有的 Python 包。 |
| / 功能 = SQL_SHARED_MR | 安装独立版本的 R 功能： SQL Server 自 2017 年 1 机器学习服务器 （独立） 或 SQL Server 2016 R Server （独立）。 独立服务器是未绑定到数据库引擎实例的"共享的功能"。|
| / 功能 = SQL_SHARED_MPY | 适用于仅 SQL Server 自 2017 年。 安装独立版本的 Python 功能： SQL Server 自 2017 年 1 机器学习服务器 （独立）。 独立服务器是未绑定到数据库引擎实例的"共享的功能"。|
| /IACCEPTROPENLICENSETERMS  | 指示已接受使用的开放源代码 R 组件的许可条款。 |
| / IACCEPTPYTHONLICENSETERMS | 指示已接受使用 Python 组件的许可条款。 |
| /IACCEPTSQLSERVERLICENSETERMS | 指示已接受使用 SQL Server 的许可条款。|
| / MRCACHEDIRECTORY | 脱机安装程序，将设置包含的 R 组件 CAB 文件的文件夹。 |
| / MPYCACHEDIRECTORY | 脱机安装程序，将设置包含的 Python 组件 CAB 文件的文件夹。 |


## <a name="indb"></a> 数据库实例安装

数据库中分析是可供数据库引擎实例，所需的添加**AdvancedAnalytics**到你的安装的功能。 您可以使用高级分析，安装数据库引擎实例或[将其添加到现有实例](#add-existing)。 

若要查看进度信息，而不需要交互式屏幕提示，请使用 /qs 参数。

> [!IMPORTANT]
> 安装完成后，保持两个其他配置步骤。 直到执行这些任务，才会完成集成。 请参阅[安装后任务](#post-install)有关的说明。

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017： 数据库引擎，高级分析具有 Python 和 R

对于数据库引擎实例的并发安装，提供的实例名称和管理员 (Windows) 登录名。 包括用来安装核心和语言组件，以及所有的许可条款的接受功能。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此相同的命令，但带有上数据库引擎使用的 SQL Server 登录混合身份验证。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

此示例仅 Python，显示，你可以通过省略功能中添加一种语言。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016： 数据库引擎和使用 R 的高级的分析

此命令是相同 SQL Server 自 2017 年，但不 Python 元素，这是不在 SQL Server 2016 安装程序。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 安装后配置 （必需）

适用于数据库中仅安装。

在安装完成时，可以使用 R 和 Python、 Microsoft R 和 Python 包、 Microsoft R Open、 Anaconda、 工具、 示例和属于分发的脚本的数据库引擎实例。 

需要执行两个多个任务以完成安装：

1. 重新启动数据库引擎服务。

1. 你可以使用功能之前，请启用外部脚本。 按照中的说明[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](sql-machine-learning-services-windows-install.md)作为下一步。 

为 SQL Server 2016，请改用本文[安装 SQL Server 2016 R Services （数据库）](sql-r-services-windows-install.md)。

## <a name="add-existing"></a> 将高级分析功能添加到现有的数据库引擎实例

在添加到现有的数据库引擎实例数据库中的高级的分析，提供实例名称。 例如，如果你以前安装的 SQL Server 2017 数据库引擎和 Python，你可以使用此命令以添加。

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 无提示安装

无提示安装取消.cab 文件位置的检查。 为此，你必须指定.cab 文件要解包的位置。 为此，你可以临时目录。
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> 独立服务器安装

独立服务器是未绑定到数据库引擎实例的"共享的功能"。 下面的示例演示这两个版本的有效语法。

SQL Server 2017 支持独立的服务器上的 Python 和 R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 是仅 R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

完成安装程序后，你有一台服务器、 Microsoft 包、 R 和 Python，工具，示例和脚本，属于分发的开源分发。 

若要打开 R 控制台窗口，请转到 files\microsoft SQL Server\140 （或 130） \R_SERVER\bin\x64，然后双击**RGui.exe**。 不熟悉 R？ 此教程：[基本 R 命令和 RevoScaleR 函数： 25 的常见示例](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler)。

若要打开 Python 命令，请转到 files\microsoft SQL Server\140\PYTHON_SERVER\bin\x64，然后双击**python.exe**。

## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并修复常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何使用 SQL Server 的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [针对 R 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 用于 SQL Server 按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。