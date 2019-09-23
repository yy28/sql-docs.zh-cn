---
title: 适用于 SQL Server、Azure SQL （Azure SQL 数据库、Azure SQL 托管实例、SQL 虚拟机）和 Azure SQL 数据仓库的 SQL 查询和管理工具 |Microsoft Docs
description: 适用于 SQL Server、Azure SQL （Azure SQL 数据库、Azure SQL 托管实例、SQL 虚拟机）和 Azure SQL 数据仓库的 SQL 查询和管理工具
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 09/11/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 9c5262dfc610e62f0782b0cc6c8fe523d94d0730
ms.sourcegitcommit: c0fd28306a3b42895c2ab673734fbae2b56f9291
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71096874"
---
# <a name="sql-query-and-management-tools-for-sql-server"></a>SQL Server 的 SQL 查询和管理工具

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要管理（查询、监视等）数据库，需要一个工具。 虽然数据库可以在云中、Windows 上或 [Linux](../linux/sql-server-linux-overview.md) 上运行，但工具不需与数据库在相同的平台上运行。

有许多可用的数据库工具，因此本文提供的说明和指南介绍了一些可用于处理 SQL 数据库的工具。 如果不知道如何确定所需的工具，请参阅[应使用哪种工具？](#which-tool-should-i-choose)。

有关其他信息以及要下载工具，请在下表中选择 "工具" 列中的链接。 若要下载 SQL Server，请参阅[安装 SQL Server](../database-engine/install-windows/install-sql-server.md)。

## <a name="gui-tools-to-manage-databases"></a>管理数据库的 GUI 工具

以下工具提供了图形用户界面（GUI）：

| 工具 | 描述 | 运行平台 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] 是一款轻型免费工具，用于管理数据库，无论数据库在何处运行。 此预览版提供各种数据库管理功能，其中包括扩展的 Transact-SQL 编辑器以及可自定义的数据库操作状态见解。 | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、macOS 和 Linux 上运行**。|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | 使用 SQL Server Management Studio (SSMS) 查询、设计和管理你的 SQL Server、Azure SQL 数据库和 Azure SQL 数据仓库。 | **SSMS 在 Windows 上运行**。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | 将 Visual Studio 变成适用于 SQL Server、Azure SQL 数据库和 Azure SQL 数据仓库的强大开发环境。| **SSDT 在 Windows 上运行**。|
| [Visual Studio Code](https://code.visualstudio.com/)| 在安装 Visual Studio Code 之后, 请安装用于开发 Microsoft SQL Server、Azure SQL 数据库和 SQL 数据仓库的 [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)。| **Visual Studio Code 在 Windows、macOS 和 Linux 上运行**。|

## <a name="command-line-tools-to-manage-databases"></a>用于管理数据库的命令行工具

下面是主要的命令行工具:

| 工具 | 描述 | 运行平台 |
|:--|:--|:--|
|[**mssql-cli（预览版）** ](mssql-cli.md)|**mssql-cli** 是一项用于查询 SQL Server 的交互式命令行工具。 | Windows、macOS 和 Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage**是一个命令行实用工具, 可自动执行多个数据库开发任务。 sqlpackage 的 macOS 和 Linux 版本目前为预览版。 | Windows、macOS 和 Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** 提供了用于处理 SQL 的 cmdlet| Windows、macOS 和 Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd**实用工具允许您在命令提示符下输入 transact-sql 语句、系统过程和脚本文件。 | Windows、macOS 和 Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|大容量复制程序实用工具 (bcp) 可以在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例和用户指定格式的数据文件间大容量复制数据     。|Windows、macOS 和 Linux|
|[**mssql-脚本程序 (预览版)** ](https://github.com/Microsoft/mssql-scripter)|**mssql-脚本**编写是用于脚本 SQL Server 数据库的多平台命令行体验|Windows、macOS 和 Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql-conf** 配置在 Linux 上运行的 SQL Server。|Linux|

## <a name="which-tool-should-i-choose"></a>我应该选择哪种工具？

- 想要在 Windows、Linux 或 Mac 上的轻型编辑器中管理 SQL Server 实例或数据库？ 请选择 [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- 想要在具有完整 GUI 支持的 Windows 上管理 SQL Server 实例或数据库？ 请选择 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- 想要创建或维护数据库代码，包括 Windows 上的编译时验证、重构和设计器支持？ 请选择 [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- 想要使用具有 IntelliSense、语法高亮等功能的命令行工具查询 SQL Server？ 请选择 [mssql-cli](mssql-cli.md)
- 想要在 Windows、Linux 或 Mac 上的轻型编辑器中编写 T-SQL 脚本？ 请选择 [Visual Studio Code](https://code.visualstudio.com/) 和 [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="additional-tools"></a>其他工具

| 工具 | 描述 |
|:--|:--|
| [配置管理器](../tools/configuration-manager/sql-server-configuration-manager-help.md) | 使用 SQL Server 配置管理器配置 SQL Server 服务并配置网络连接。 Configuration Manager 在 Windows 上运行|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | 使用 SQL Server Migration Assistant 自动将数据库从 Microsoft Access、DB2、MySQL、Oracle 和 Sybase 迁移到 SQL Server。|
| [数据库实验助手](../dea/database-experimentation-assistant-overview.md) | 使用数据库实验助手评估给定工作负荷的 SQL 的目标版本。 |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | 使用 Distributed Replay 功能可帮助你评估将来 SQL Server 升级的影响。 还可以使用 Distributed Replay 帮助评估硬件和操作系统升级的影响, 以及 SQL Server 优化。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 实用程序在 Service Broker 服务的 Service Broker 会话或配置中报告问题。 |

如果你正在寻找此页面未提及的其他工具, 请参阅[SQL 命令提示实用工具](command-prompt-utility-reference-database-engine.md)。