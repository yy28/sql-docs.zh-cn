---
title: "从命令行安装 Microsoft R Server | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 87d6c0b358d7747b20ed37f159e713cc10018866
ms.contentlocale: zh-cn
ms.lasthandoff: 09/21/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>从命令行安装 Microsoft R Server
    
本主题介绍如何使用 SQL Server 命令行自变量以在 SQL Server 2016 中安装 Microsoft R Server 或者在 SQL Server 2017 安装机器学习 Server （独立）。 

> [!NOTE]
也可以使用单独的 Windows installer 来安装 Microsoft R Server。 有关详细信息，请参阅[安装 R Server 9.0.1 for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 

## <a name="prerequisites"></a>先决条件

这种安装方法需要您知道如何执行 SQL Server 的命令行安装，并熟悉其脚本的自变量。

- **无人参与** 安装要求指定安装实用程序的位置，并使用参数指示要安装的功能。 
- 对于 **静默** 安装，提供相同的参数并添加 **/q** 切换。 不提供提示，无需交互。 但是，如果遗漏了任何所需的参数，安装将失败。

有关详细信息，请参阅 [从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQL Server 2017: Microsoft 机器学习 Server （独立）

运行以下命令从提升的命令提示符安装仅 Microsoft 机器学习 Server （独立） 和其必备组件。  该示例演示使用来安装。 的自变量

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

若要查看进度和提示，请删除 _/q_ 参数。

- **功能 = SQL_SHARED_MR**获取仅的机器学习服务器组件。 这包括所有必备组件，默认情况下无提示安装。
- **SQL_INST_MR**都不必 installl R 语言的支持。
- **SQL_INST_MPY**安装 for Python 支持所需。
- **IACCEPTROPENLICENSETERMS** 指示已接受使用开放源 R 组件的许可证条款。
- **IACCEPTPYTHONLICENSETERMS**指示已接受使用 Python 组件的许可条款。
- 运行安装向导需要**IACCEPTSQLSERVERLICENSETERMS** 。

**说明**

1. 功能参数是必需的，与 SQL Server 许可条款。
2. 指定至少一种语言，以及许可协议标志。
3. 你可以安装一个语言中，或同时 R 和 Python，但要求为每个单独的许可证。

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQL Server 2016: Microsoft R Server （独立）

从提升的命令提示符运行以下命令，仅安装 Microsoft R Server（独立版）及其必备组件。  以下示例显示与 SQL Server 2016 安装程序使用的自变量。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>脱机安装

如果在没有 Internet 访问的计算机上安装机器学习服务器或 Microsoft R Server （独立），必须提前下载所需的 R 组件，并将它们复制到本地文件夹。 有关下载位置，请参阅 [在没有 Internet 连接的情况下安装 R 组件](../r/installing-ml-components-without-internet-access.md)。

## <a name="what-is-installed"></a>安装的内容

安装程序完成后，可以查看 SQL Server 安装程序创建的配置文件以及安装程序操作的摘要。

默认情况下，所有 SQL server 安装日志和摘要，并在以下文件夹中创建相关的功能：

- SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- SQL Server 自 2017 年 1:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

为每个已安装功能创建单独的子文件夹。

若要设置的 Microsoft R Server 具有相同参数的另一个实例，可以重新使用在安装期间创建的配置文件。 有关详细信息，请参阅[使用配置文件安装 SQL Server](/sql-docs/docs/database-engine/install-windows/install-sql-server-2016-using-a-configuration-file)


## <a name="customize-your-r-environment"></a>自定义 R 环境

安装完成后，可以安装其他 R 包。 有关详细信息，请参阅 [安装和管理 R 包](../r/install-additional-r-packages-on-sql-server.md)。

> [!IMPORTANT]
> 如果你想要在 SQL Server 上运行 R 代码，请确保你将使用有关在开发解决方案，并将执行或部署解决方案的位置的 SQL Server 实例的计算机上安装相同的包。

安装 （数据库） 的机器学习服务后，你可以使用单独的 Windows installer，将指定的 SQL Server 实例相关联的 R 版本升级。 有关详细信息，请参阅[到升级 R 使用 SqlBindR](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。



