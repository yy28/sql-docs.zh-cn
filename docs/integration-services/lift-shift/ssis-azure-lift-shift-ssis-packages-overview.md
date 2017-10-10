---
title: "提升和移动到云中的 SQL Server Integration Services 工作负荷 |Microsoft 文档"
ms.date: 10/09/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 85ab11747276f0c6c58b13cd409df3e5774915ae
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>提升和移动到云中的 SQL Server Integration Services 工作负荷
现在可以将你的 SQL Server Integration Services (SSIS) 包和工作负荷移动到 Azure 云。
-   存储和管理 SSIS 项目和 Azure SQL 数据库上的 SSIS 目录数据库 (SSISDB) 中的包。
-   在 Azure SSIS 的集成运行库，作为 Azure 数据工厂版本 2 的一部分引入的实例中运行包。
-   有关这些通用任务使用熟悉的工具如 SQL Server Management Studio (SSMS)。

## <a name="benefits"></a>优势
将本地 SSIS 工作负荷移至 Azure 具有以下潜在的好处：
-   **降低运营成本**通过减少本地基础结构。
-   **增加高可用性**与每个群集，以及高可用性功能的 Azure 和 Azure SQL 数据库的多个节点。
-   **提高可伸缩性**能够指定每个节点 （纵向扩展） 的多个核心和每个群集 （横向扩展） 的多个节点。
-   **避免限制**的 Azure 虚拟机上运行 SSIS。

## <a name="architecture-overview"></a>体系结构概述
下表列出了在本地的 SSIS 和在 Azure 上的 SSIS 之间的差异。 最重要的差异是存储分离与计算。

| 存储器 | 运行时 | 可伸缩性 |
|---|---|---|
| 在本地 (SQL Server) | SQL Server 托管的 SSIS 运行时 | SSIS 向外扩展 （SQL Server 2017 及更高版本）<br/><br/>自定义解决方案 （在之前版本的 SQL Server） |
| 在 Azure （SQL 数据库） 上 | Azure SSIS 运行集成时，Azure 数据工厂版本 2 的组件 | SSIS ir 的缩放选项 |
| | | |

Azure 数据工厂承载在 Azure 上的 SSIS 包的运行时引擎。 运行时引擎调用 Azure SSIS 集成运行库 (SSIS IR)。

当您设置 SSIS IR 时，可以向上扩展和横向扩展，通过指定以下选项的值：
-   （包括的内核数） 的节点大小和群集中的节点数。
-   Azure SQL 数据库来承载 SSIS 目录数据库 (SSISDB) 和数据库的服务层的现有实例。
-   每个节点最大并行执行。

只需设置一次的 SSIS IR。 之后，您可以使用熟悉的工具，如 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 若要部署，配置、 运行、 监视、 计划和管理包。

> [!NOTE]
> 在此公共预览期间 Azure SSIS 集成运行时才可用在美国东部和欧洲北部区域中。

数据工厂还支持其他类型的集成运行时。 若要了解有关 SSIS IR 和集成运行时的其他类型的详细信息，请参阅[集成运行库在 Azure 数据工厂中的](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)。

## <a name="prerequisites"></a>先决条件
本主题中所述的功能需要 SQL Server Data Tools (SSDT) 版本 17.2 或更高版本，但不是需要 SQL Server 2017 或 SQL Server 2016。 当将包部署到 Azure 时，包部署向导始终的包升级到最新的包格式。

有关在 Azure 中的先决条件的详细信息，请参阅[提起并移动到 Azure 包 SQL Server Integration Services (SSIS)](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

## <a name="ssis-features-on-azure"></a>在 Azure 上的 SSIS 功能

当设置要承载 SSISDB 的 SQL 数据库实例时，安装 Azure Feature Pack for SSIS 和访问可再发行。 这些组件提供连接到 Excel 和 Access 文件和各种 Azure 数据源。 在此时间，不能用于 SSIS 安装第三方组件。

承载 SSISDB 的 SQL 数据库名称将成为由四部分构成的名称，部署和从 SSDT 和 SSMS 的管理包时要使用的第一部分`<sql_database_name>.database.windows.net`。

必须将项目部署模型，不使用包部署模型，用于将部署到 Azure SQL 数据库上的 SSISDB 的项目。

你继续设计和构建包本地在 SSDT 中，或在 Visual Studio 中使用 SSDT 安装。

有关如何从使用 Windows 身份验证云连接到本地数据源的信息，请参阅[连接到本地数据源使用 Windows 身份验证](ssis-azure-connect-with-windows-auth.md)。

## <a name="common-tasks"></a>常规任务

### <a name="provision"></a>预配
可以部署，还可以在 Azure 中运行 SSIS 包之前，必须设置 SSISDB 目录数据库和 Azure SSIS 集成运行库。 按照在本文中的设置步骤：[提起并移动到 Azure 包 SQL Server Integration Services (SSIS)](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

### <a name="deploy-and-run-packages"></a>部署和运行包
若要将项目部署和 SQL 数据库上运行包，可以使用几种熟悉的工具和脚本选项之一：
-   SQL Server Management Studio (SSMS)
-   Transact SQL （从 SSMS、 Visual Studio 代码或另一种工具）
-   命令行工具
-   PowerShell
-   C# 和 SSIS 管理对象模型

### <a name="monitor-packages"></a>监视包
若要监视正在运行的包，在 SSMS 中，可以在 SSMS 中使用以下报表的工具之一。
-   右键单击**SSISDB**，然后选择**活动操作**以打开**活动操作**对话框。
-   在对象资源管理器，右键单击并选择中选择包**报表**，然后**标准报表**，然后**所有执行**。

### <a name="schedule-packages"></a>计划包
若要计划的执行的 SQL 数据库中存储的包，可以使用以下工具：
-   本地 SQL Server 代理
-   数据工厂 SQL Server 存储过程活动

有关详细信息，请参阅[计划 SSIS 包在 Azure 上的执行](ssis-azure-schedule-packages.md)。

## <a name="next-steps"></a>后续步骤
若要开始使用 Azure 上的 SSIS 工作负荷，请参阅以下文章：
-   [提起并移动到 Azure 的 SQL Server Integration Services (SSIS) 包](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [部署、 运行和监视在 Azure 上的 SSIS 包](ssis-azure-deploy-run-monitor-tutorial.md)

