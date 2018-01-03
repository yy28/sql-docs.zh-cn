---
title: "从命令行安装机器学习 Server （独立） 或 Microsoft R Server （独立） |Microsoft 文档"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c10594fdecd48782a80b5d609bb21c6a937f8863
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>从命令行安装机器学习 Server （独立） 或 Microsoft R Server （独立）

本文介绍如何使用 SQL Server 命令行自变量以通过使用命令行安装以下 SQL Server 功能：

+ [SQL Server 自 2017 年中的计算机学习 Server （独立）](#bkmk_mls2017) 
+ [SQL Server 2016 中的 Microsoft R Server （独立）](#bkmk_mrs2016)

**无人参与**安装需要你指定的位置安装实用程序，并使用参数来指示要安装的功能。

对于 **静默** 安装，提供相同的参数并添加 **/q** 切换。 不提供任何提示，无需交互即可。 如果省略任何所需的参数，但是，安装程序将失败。

## <a name="prerequisites"></a>必备条件

你应知道如何执行 SQL Server 的命令行安装，并熟悉其脚本的自变量。

有关详细信息，请参阅[从命令提示符安装 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。

如果在没有 Internet 访问的计算机上安装机器学习服务器或 Microsoft R Server （独立），必须提前下载所需的 R （或 Python） 组件，并将它们复制到本地文件夹。 有关下载位置，请参阅[安装没有 internet 访问权限的机器学习组件](installing-ml-components-without-internet-access.md)。


## <a name="bkmk_mls2017"></a>安装 Microsoft 机器学习 Server （独立）

**适用于： SQL Server 自 2017 年 1**

运行以下命令从提升的命令提示符安装仅机器学习服务器 （独立） 和其必备组件。

+ 功能参数是必需的，与 SQL Server 许可条款。
+ 你可以安装一个语言中，或同时 R 和 Python，但要求为每个单独的许可证。

此示例演示使用来安装。 的自变量

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

此示例演示使用若要安装 Python 的自变量。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ 若要查看进度和提示，请删除 _/q_ 参数。
+ 如果使用自变量**功能 = SQL_SHARED_MR**，安装仅的机器学习服务器组件，并使用 R 和 Python 都不。 此安装过程中包括所有系统必备组件，默认情况下无提示安装。 但是，建议你在第一次安装时添加至少一种语言。
+ 添加**SQL_INST_MR**来安装。 的支持
+ 添加**SQL_INST_MPY**来安装 Python 的支持。
+ **IACCEPTROPENLICENSETERMS** 指示已接受使用开放源 R 组件的许可证条款。
+ **IACCEPTPYTHONLICENSETERMS**指示已接受使用 Python 组件的许可条款。
+ 运行安装向导需要**IACCEPTSQLSERVERLICENSETERMS** 。


## <a name="bkmk_mrs2016"></a>安装 Microsoft R Server（独立版）

**适用于： SQL Server 2016**

运行以下命令从提升的命令提示符安装**仅**Microsoft R Server （独立） 和其必备组件。 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> 我们建议你不要不安装这同一台计算机承载 SQL Server R Services 的实例上。

## <a name="post-installation-tasks"></a>安装后任务

若要设置的 Microsoft R Server 具有相同参数的另一个实例，可以重新使用在安装期间创建的配置文件。 有关详细信息，请参阅[使用配置文件安装 SQL Server](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)。

### <a name="review-installed-components"></a>查看安装组件

安装程序完成后，可以查看 SQL Server 安装程序创建的配置文件以及安装程序操作的摘要。

默认情况下，所有 SQL server 安装日志和摘要，并在以下文件夹中创建相关的功能：

+ SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

为你安装每项功能创建一个单独的子文件夹。

### <a name="customize-the-r-or-python-environment"></a>自定义 R 或 Python 环境

安装完成后，你可以安装其他 R 或 Python 包。 根据你使用的 SQL Server 2016 或 SQL Server 2017 某种程度上，则流程不同。

在 SQl Server 自 2017 年，你可以安装和管理通过使用 T-SQL 的 R 包。 有关详细信息，请参阅[安装和管理 R 包](../r/install-additional-r-packages-on-sql-server.md)。

Python，并在 SQL Server 2016 中，管理员必须安装可能需要的任何其他库。

> [!IMPORTANT]
> 如果你想要在 SQL Server 上运行 R 代码，请确保你将使用有关在开发解决方案，并将执行或部署解决方案的位置的 SQL Server 实例的计算机上安装相同的包。

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>升级 R Server 或 SQL Server 机器学习

如果不打算使用 SQL Server，你可以使用单独的 Windows installer 来安装 Microsoft R Server 或机器学习服务器。 有关下载位置和说明，请参阅以下链接：

+ [安装机器学习适用于 Windows 的服务器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安装 R Server 9.0.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

单独的 windows installer 机器学习服务器还可以用于升级机器学习与实例关联的组件。  有关详细信息，请参阅以下链接：

+ [使用 SqlBindR 升级 R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
