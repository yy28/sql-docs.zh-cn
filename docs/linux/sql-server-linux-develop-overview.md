---
title: 为 Linux 上的 SQL Server 开发应用程序 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 4d3ef46dfbacb1c4cbfe67df555b79fb10ade86d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705813"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>如何为 Linux 上的 SQL Server 开发应用程序

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以创建应用程序连接到 SQL Server Linux 上和使用从各种编程语言，如C#、 Java、 Node.js、 PHP、 Python、 Ruby 和C++。 还可使用流行的 Web 框架和对象关系映射 (ORM) 框架。

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 用户还可使用这些相同的开发选项面向其他平台上的 SQL Server。 应用程序可面向本地或云中、在 Linux、Windows 或 macOS 上的 Docker 中运行的 SQL Server。 也可面向 Azure SQL 数据库和 Azure SQL 数据仓库。

## <a name="try-the-tutorials"></a>请按教程进行尝试

熟悉和使用 SQL Server 生成应用程序的最佳方式就是自己亲自尝试。

- 浏览到[入门教程](https://aka.ms/sqldev)。
- 选择语言和开发平台。
- 尝试代码示例。

> [!TIP]
> 如果你想要开发适用于 Docker 上的 SQL Server，看一看**macOS**教程。

## <a name="create-new-applications"></a>创建新的应用程序

如果要创建新的应用程序，看看一系列[连接库](sql-server-linux-develop-connectivity-libraries.md)有关连接器和常用的框架可用于各种编程语言的摘要。

## <a name="use-existing-applications"></a>使用现有应用程序

如果有现有的数据库应用程序，您可以到目标 Linux 上的 SQL Server 只需更改其连接字符串。 请务必阅读有关[已知问题](sql-server-linux-release-notes.md)Linux 上的 SQL Server 中。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>通过 Linux 上的 SQL Server 使用 Windows 上的现有 SQL 工具

当前在如 SSMS、 SSDT 和 PowerShell，Windows 运行的工具也适用于 Linux 上的 SQL Server。 尽管它们不可在本机 Linux 上运行，但你仍然可以管理 Linux 上的远程 SQL Server 实例。 

有关详细信息，请参阅下列主题：

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 为获得最佳体验，请确保使用最新版本的工具。

## <a name="use-new-sql-tools-for-linux"></a>使用适用于 Linux 的新 SQL 工具

你可以使用新[mssql 扩展](https://aka.ms/mssql-marketplace)有关[Visual Studio Code](https://code.visualstudio.com)在 Linux、 macOS 和 Windows。 相关分布演练请参阅下列教程：

- [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)

还可使用对 Linux 而言属于本机的新命令行工具。 这些工具包括：

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>后续步骤

若要开始，请使用以下快速入门教程之一在 Linux 上安装 SQL Server：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
