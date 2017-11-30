---
title: "开发应用程序的 SQL Server on Linux |Microsoft 文档"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 11/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.workload: On Demand
ms.openlocfilehash: aa5b8ecf8b9801874d0af342d268073a09e4812c
ms.sourcegitcommit: 28cccac53767db70763e5e705b8cc59a83c77317
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2017
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>如何为 Linux 上的 SQL Server 开发应用程序

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

你可以创建应用程序连接到并从多种编程语言，如 C#、 Java、 Node.js、 PHP、 Python、 Ruby 和 c + + Linux 上使用 SQL Server 自 2017 年。 还可使用流行的 Web 框架和对象关系映射 (ORM) 框架。

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 用户还可使用这些相同的开发选项面向其他平台上的 SQL Server。 应用程序可面向本地或云中、在 Linux、Windows 或 macOS 上的 Docker 中运行的 SQL Server。 也可面向 Azure SQL 数据库和 Azure SQL 数据仓库。

## <a name="try-the-tutorials"></a>请按教程进行尝试

熟悉和使用 SQL Server 生成应用程序的最佳方式就是自己亲自尝试。

- 浏览到[入门教程](http://aka.ms/sqldev)。
- 选择语言和开发平台。
- 尝试代码示例。

> [!TIP]
> 如果你想要为 Docker 上的 SQL Server 2017 开发，看一看**macOS**教程。

## <a name="create-new-applications"></a>创建新的应用程序

如果你要创建新的应用程序，看一看一份[连接库](sql-server-linux-develop-connectivity-libraries.md)有关连接器并针对各种编程语言提供的常用框架的摘要。

## <a name="use-existing-applications"></a>使用现有应用程序

如果你有现有的数据库应用程序，你可以只需改为在 Linux 上的目标 SQL Server 自 2017 年的其连接字符串。 请务必阅读有关[已知问题](sql-server-linux-release-notes.md)在 Linux 上的 SQL Server 2017。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>通过 Linux 上的 SQL Server 使用 Windows 上的现有 SQL 工具

在 Linux 上的 SQL Server 2017 还处理当前在如 SSMS、 SSDT 和 PowerShell，Windows 运行的工具。 尽管它们不可在本机 Linux 上运行，但你仍然可以管理 Linux 上的远程 SQL Server 实例。 

有关详细信息，请参阅下列主题：

- [SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note] 
> 为获得最佳体验，请确保使用最新版本的工具。

## <a name="use-new-sql-tools-for-linux"></a>使用适用于 Linux 的新 SQL 工具

你可以使用新[mssql 扩展](https://aka.ms/mssql-marketplace)为[Visual Studio Code](https://code.visualstudio.com) Linux、 macOS 和 Windows 上。 相关分布演练请参阅下列教程：

- [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)

还可使用对 Linux 而言属于本机的新命令行工具。 这些工具包括：

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>后续步骤

若要开始，请在使用以下快速入门教程之一的 Linux 上安装 SQL Server:

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
