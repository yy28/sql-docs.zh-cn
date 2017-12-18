---
title: "将 SQL Server Integration Services 工作负荷直接迁移到云 | Microsoft Docs"
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1fd45ef05d5469acb83a80e3463329976b9a843
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>将 SQL Server Integration Services 工作负荷直接迁移到云
现在，可将 SQL Server Integration Services (SSIS) 包和工作负荷移到 Azure 云。
-   在 Azure SQL 数据库的 SSIS 目录数据库 (SSISDB) 中，存储和管理 SSIS 项目和包。
-   在 Azure SSIS Integration Runtime（作为 Azure 数据工厂版本 2 的一部分引入）的实例中运行包。
-   针对以下常见任务，使用 SQL Server Management Studio (SSMS) 等熟悉的工具。

## <a name="benefits"></a>优势
将本地 SSIS 工作负荷移到 Azure 具有以下潜在好处：
-   降低运营成本和减轻在本地或 Azure 虚拟机上运行 SSIS 时的基础结构管理负担。
-   通过实现每个群集指定多个节点，以及 Azure 和 Azure SQL 数据库的高可用性功能，增加高可用性。
-   通过实现每个节点指定多个核心（纵向扩展）和每个群集指定多个节点（横向扩展），提高可伸缩性。

## <a name="architecture-overview"></a>体系结构概述
下表突出显示了本地 SSIS 和 Azure 上的 SSIS 之间的差异。 最显著的差异是存储与计算的分离。

| 存储器 | 运行时 | 可伸缩性 |
|---|---|---|
| 本地 (SQL Server) | SQL Server 托管的 SSIS 运行时 | SSIS Scale Out（SQL Server 2017 及更高版本中）<br/><br/>自定义解决方案（之前的 SQL Server 版本中） |
| Azure 上（SQL 数据库） | Azure SSIS Integration Runtime，Azure 数据工厂版本 2 的一个组件 | SSIS IR 的缩放选项 |
| | | |

Azure 数据工厂为 Azure 上的 SSIS 包承载运行时引擎。 运行时引擎名为 Azure SSIS Integration Runtime (SSIS IR)。

设置 SSIS IR 时，可通过指定以下选项的值，实现纵向和横向扩展：
-   群集中的节点大小（包括核心数）和节点数。
-   用于承载 SSIS 目录数据库 (SSISDB) 的 Azure SQL 数据库的现有实例，以及数据库的服务层。
-   每个节点最大并行执行数。

只需设置 SSIS IR 一次。 此后，可使用 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 等熟悉工具来部署、配置、运行、监视、计划和管理包。

> [!NOTE]
> 在此公共预览期间，暂不向任何区域提供 Azure SSIS Integration Runtime。 有关支持区域的信息，请参阅[可用产品（按区域）- Microsoft Azure](https://azure.microsoft.com/regions/services/)。

数据工厂还支持其他类型的 Integration Runtime。 若要了解关于 SSIS IR 和其他类型 Integration Runtime 的详细信息，请参阅 [Azure 数据工厂中的 Integration Runtime](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime)。

## <a name="prerequisites"></a>先决条件
本文中介绍的功能不需要 SQL Server 2017 或 SQL Server 2016。

这些功能需要以下版本的 SQL Server Data Tools (SSDT)：
-   对于 Visual Studio 2017，需要版本 15.3（预览版）或更高版本。
-   对于 Visual Studio 2015，需要版本 17.2 或更高版本。

> [!NOTE]
> 将包部署到 Azure 时，包部署向导始终将包升级到最新的包格式。

有关 Azure 中先决条件的详细信息，请参阅[将 SQL Server Integration Services (SSIS) 包直接迁移到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

## <a name="ssis-features-on-azure"></a>Azure 上的 SSIS 功能

如果要设置 SQL 数据库实例来承载 SSISDB，还需安装用于 SSIS 的 Azure 功能包和 Access 可再发行组件。 除提供与内置组件支持的数据源的连接外，这些组件还提供与 Excel 和 Access 文件和各种 Azure 数据源的连接。 暂时无法安装用于 SSIS 的第三方组件（包括 Attunity 和 SAP BI 等 Microsoft 提供的第三方组件）。

承载 SSISDB 的 SQL 数据库的名称（`<sql_database_name>.database.windows.net`）将成为四部分名称的第一部分，从 SSDT 和 SSMS 中部署和管理包时会使用到该名称。

对于要部署到 Azure SQL 数据库上 SSISDB 的项目，需要使用项目部署模型，而不是包部署模型。

继续通过使用 SSDT 或使用安装了 SSDT 的 Visual Studio ，在本地设计和生成包。

有关如何使用 Windows 身份验证从云连接到本地数据源的信息，请参阅[使用 Windows 身份验证连接到本地数据源](ssis-azure-connect-with-windows-auth.md)。

## <a name="common-tasks"></a>常规任务

### <a name="provision"></a>预配
需先设置 SSISDB 目录数据库和 Azure SSIS Integration Runtime，才能在 Azure 中部署和运行 SSIS 包。 按照后列文章中的设置步骤进行操作：[将 SQL Server Integration Services (SSIS) 包直接迁移到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

### <a name="deploy-and-run-packages"></a>部署和运行包
若要在 SQL 数据库上部署项目和运行包，可以使用以下多种熟悉的工具和脚本编写选项中的一种来实现：
-   SQL Server Management Studio (SSMS)
-   Transact-SQL（从 SSMS、Visual Studio Code 或其他工具）
-   命令行工具
-   PowerShell
-   C# 和 SSIS 管理对象模型

### <a name="monitor-packages"></a>监视包
要监视 SSMS 中运行的包，可在其中使用下列报表工具之一。
-   右键单击“SSISDB”，然后选择“活动操作”以打开“活动操作”对话框。
-   在对象资源管理器中选择包，然后依次选择“报表”、“标准报表”、“所有执行”。

### <a name="schedule-packages"></a>计划包
若要计划安排 SQL 数据库中存储的包的执行，可使用以下工具：
-   本地 SQL Server 代理
-   数据工厂 SQL Server 存储过程活动

有关详细信息，请参阅[计划安排 Azure 上的 SSIS 包执行](ssis-azure-schedule-packages.md)。

## <a name="next-steps"></a>后续步骤
若要开始使用 Azure 上的 SSIS 工作负荷，请参阅以下文章：
-   [将 SQL Server Integration Services (SSIS) 包直接迁移到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [在 Azure 上部署、运行和监视 SSIS 包](ssis-azure-deploy-run-monitor-tutorial.md)
