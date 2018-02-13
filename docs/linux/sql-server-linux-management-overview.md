---
title: "管理在 Linux 上的 SQL Server |Microsoft 文档"
description: "这篇文章提供有关 SQL Server 运行在 Linux 上的常见管理任务和工具的链接。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: de19f1952465c62bf026dbd3d92666b7a1b968ae
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>选择合适的工具管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

有多种方法来管理在 Linux 上的 SQL Server 2017。 以下部分提供不同的管理工具和技术使用指向更多资源的快速的概述。

## <a name="mssql-conf"></a>mssql-conf 
**Mssql conf**工具在 Linux 上配置 SQL Server。 有关详细信息，请参阅[mssql conf 与 Linux 上配置 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

几乎所有在客户端工具中可以完成的工作，都可以使用 Transact - SQL 语句来完成。 SQL Server 提供[动态管理视图 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) ，查询的状态和配置 SQL Server。 也有[TRANSACT-SQL 命令](https://msdn.microsoft.com/library/bb510741.aspx)数据库管理任务。 你可以在任何客户端工具中支持连接到 SQL Server 和运行 TRANSACT-SQL 查询，例如运行这些命令[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

## <a name="sql-server-operations-studio-preview"></a>SQL Server 操作 Studio （预览版）

新的 Microsoft SQL 操作 Studio （预览版） 是用于管理 SQL Server 的跨平台工具。 有关详细信息，请参阅[Microsoft SQL 操作 Studio （预览版）](../sql-operations-studio/what-is.md)。

## <a name="sql-server-management-studio-on-windows"></a>Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是一款 Windows 应用程序，它提供了一种用于管理 SQL Server 的图形用户界面。 尽管当前它只能在 Windows 上运行，但用户可以通过该应用程序远程连接到 Linux SQL Server 实例。 有关使用 SSMS 管理 SQL Server 的详细信息，请参阅[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

## <a name="mssql-cli-preview"></a>mssql cli （预览版）

Microsoft 已为 SQL Server 发布新的跨平台脚本编写工具[mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。 此工具当前处于预览状态。

## <a name="powershell"></a>PowerShell

PowerShell 提供了丰富的命令行环境，用于管理 Linux 上的 SQL Server。 有关详细信息，请参阅[管理 Linux 上的 SQL server 使用 PowerShell](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>后续步骤

在 Linux 上 SQL Server 的详细信息，请参阅[在 Linux 上的 SQL Server](sql-server-linux-overview.md)。
