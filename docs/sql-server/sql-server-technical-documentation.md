---
title: SQL Server 文档 | Microsoft Docs
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
monikerRange: '>= sql-server-2014 || = sqlallproducts-allversions'
ms.openlocfilehash: 06ccc15f14599c1d9861af90d6a56d65b71e3e0e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="sql-server-documentation"></a>SQL Server 文档
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 是 Microsoft 数据平台的核心部分。 SQL Server 在操作数据库管理系统 (ODBMS) 中处于领先水平。 本文档可帮助你安装、配置和使用 SQL Server。 内容包括端到端示例、代码示例和视频。 有关 SQL Server 语言的主题，请参阅 [语言参考](../t-sql/language-reference.md)。

::: moniker range="=sql-server-2017"
|新增功能  | 发行说明  |
|---------|---------|
|[SQL Server 2017 的新增功能](../sql-server/what-s-new-in-sql-server-2017.md)     | [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)        |
::: moniker-end
::: moniker range="=sql-server-2016"
|新增功能  | 发行说明  |
|---------|---------|
|[SQL Server 2016 中的新增功能](../sql-server/what-s-new-in-sql-server-2016.md)     | [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)        |
::: moniker-end

::: moniker range="=sql-server-2014"
![info_tip](../sql-server/media/info-tip.png) SQL Server 2014 内容很快会合并到 .docs 站点中。  现在，请参阅：
- [SQL Server 2014 联机丛书](https://msdn.microsoft.com/en-us/library/ms130214(v=sql.120).aspx)
- [SQL Server 2014 中的新增功能](https://msdn.microsoft.com/library/bb500435(v=sql.120).aspx)
- [SQL Server 2014 Release Notes](../sql-server/sql-server-2014-release-notes.md)
- [先前版本](https://docs.microsoft.com/en-us/previous-versions/sql/)
::: moniker-end

**试用 SQL Server！**
    + [![从评估中心下载](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477)[下载 SQL Server](http://go.microsoft.com/fwlink/?LinkID=829477)
    + [![从评估中心下载](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [下载 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
    + [![从评估中心下载](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [下载 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
    + [![创建虚拟机](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [获取具有 SQL Server 的虚拟机](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

::: moniker range=">=sql-server-2016 || = sqlallproducts-allversions"
## <a name="sql-server-technologies"></a>SQL Server 技术

|||
|-|-|
|![SQL 数据库引擎](../sql-server/media/sql-database-engine.png "SQL 数据库引擎")|**[数据库引擎](../database-engine/sql-server-database-engine-overview.md)**<br /><br /> 数据库引擎是用于存储、处理和保护数据的核心服务。 数据库引擎提供了受控访问和快速事务处理，以满足企业内最苛刻的数据消费应用程序的要求。 数据库引擎还提供了大量的支持以保持高可用性。|
|![R Server](../sql-server/media/r-server.png "R Server")|**[机器学习服务](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft 机器学习服务支持使用常用 R 和 Python 语言，将机器学习集成到企业工作流中。<br /><br /> 机器学习服务（数据库内）将 R 和 Python 与 SQL Server 集成，方便用户通过调用存储过程，轻松生成、重新定型模型，并对模型评分。  Microsoft 机器学习服务器对 R 和 Python 提供企业级支持，用户无需使用 SQL Server。|
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一个生成高性能数据集成解决方案的平台，其中包括对数据仓库提供提取、转换和加载 (ETL) 处理的包。|
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] 是一个针对个人、团队和公司商业智能的分析数据平台和工具集。 服务器和客户端设计器通过使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]、Excel 和 SharePoint Server 环境，支持传统的 OLAP 解决方案、新的表格建模解决方案以及自助式分析和协作。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还包括数据挖掘，以便你可以发现隐藏在大量数据中的模式和关系。|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services 提供启用了 Web 的企业级报告功能。  从而使用户可以创建从多个数据源提取数据的表，发布各种格式的表，以及集中管理安全性和订阅。|
|![复制服务](../sql-server/media/replication-services.png "复制服务")|**[复制](../relational-databases/replication/sql-server-replication.md)**<br /><br /> 复制是一组技术，用于在数据库间复制和分发数据和数据库对象，然后在数据库间进行同步操作，使其保持一致。 使用复制时，可以通过局域网和广域网、拨号连接、无线连接和 Internet，将数据分发到不同位置以及分发给远程用户或移动用户。|
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) 为你提供知识驱动型数据清理解决方案。 DQS 使您可以生成知识库，然后使用此知识库，同时采用计算机辅助方法和交互方法，执行数据更正和消除重复的数据。 您可以使用基于云的引用数据服务，并可以生成一个数据管理解决方案将 DQS 与 SQL Server Integration Services 和 Master Data Services 相集成。|
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 是用于主数据管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 解决方案。 基于 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 生成的解决方案可帮助确保报表和分析均基于适当的信息。 使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]，您可以为主数据创建中央存储库，并随着主数据随时间变化而维护一个可审核的安全对象记录。|
::: moniker-end

## <a name="migrate-and-move-data"></a>迁移和移动数据

- [使用 SQL Server 导入和导出向导导入和导出数据](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)
- [Microsoft 数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)
- [将 SQL Server 数据库迁移至 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

## <a name="update-your-version-of-sql-server"></a>更新 SQL Server 的版本

- [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx) 链接和有关所有受支持版本的信息

## <a name="samples"></a>示例

- [Wide World Importers 示例数据库](https://docs.microsoft.com/en-us/sql/samples/wide-world-importers-what-is)
- [适用于 SQL Server 2016 的 AdventureWorks 示例数据库和脚本](https://docs.microsoft.com/en-us/sql/samples/sql-samples-where-are) 
- [GitHub 上的 SQL Server 示例](https://github.com/Microsoft/sql-server-samples)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]