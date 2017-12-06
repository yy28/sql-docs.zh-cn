---
title: "SQL 工具和实用程序可用于 SQL Server、 Azure SQL Database 和 Azure SQL 数据仓库 |Microsoft 文档"
ms.custom: 
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: "0"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ba7958a1b5b9398dec3cb07630ee84b72970d2ae
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL 工具和实用程序可用于 SQL Server、 Azure SQL Database 和 Azure SQL 数据仓库
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]  


## <a name="tools-to-run-queries-and-manage-databases"></a>工具来运行查询和管理数据库  

| 工具 | Description |
|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]是一个免费的轻量的工具，用于管理数据库，只要它们正在运行。 此预览版中提供数据库管理功能，包括扩展的 TRANSACT-SQL 编辑器和可自定义深入了解你的数据库的操作状态。 **[!INCLUDE[name-sos](../includes/name-sos-short.md)]在 Windows、 macOS 和 Linux 上运行**。|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | 使用 SQL Server Management Studio (SSMS) 来查询、 设计和管理 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库。 **在 Windows 上运行 SSMS**。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | 将 Visual Studio 的 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库转换功能强大的开发环境中。 **在 Windows 上运行 SSDT**。|
| [Visual Studio 代码](https://code.visualstudio.com/)| 在安装 Visual Studio Code 之后, 安装[mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)用于开发 Microsoft SQL Server、 Azure SQL 数据库和 SQL 数据仓库。 **在 Windows、 macOS 和 Linux 上运行 visual Studio Code**。|



## <a name="additional-tools"></a>其他工具

| 工具 | Description |
|:--|:--|
| [配置管理器](../tools/configuration-manager/sql-server-configuration-manager-help.md) | 使用 SQL Server 配置管理器来配置 SQL Server 服务和配置网络连接。|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | 用于 SQL Server Migration Assistant 自动执行数据库迁移到 SQL Server 从 Microsoft Access、 DB2、 MySQL、 Oracle 和 Sybase。|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | 使用分布式重播功能来帮助你评估 SQL Server 的将来的升级的影响。 此外可以使用分布式重播来帮助评估的硬件和操作系统升级和 SQL Server 优化的影响。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 实用工具将报告 Service Broker 对话或 Service Broker 服务的配置中的问题。 |


## <a name="command-line-utilities"></a>命令行实用工具

  命令行实用工具使您能够在脚本[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]操作。 下表包含了随 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供的命令提示实用工具列表。  
  
|**实用工具**|**说明**|**安装位置**|  
|-----------------|---------------------|----------------------|  
|[bcp 实用工具](../tools/bcp-utility.md)|用于在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例和用户指定格式的数据文件之间复制数据。|\<*驱动器*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 实用工具](../tools/dta/dta-utility.md)|用于分析工作负荷并建议物理设计结构，以优化该工作负荷下的服务器性能。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 实用工具](../integration-services/packages/dtexec-utility.md)|用于配置和执行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。 该命令提示实用工具的用户界面版本称为 **DTExecUI**，它可提供执行包实用工具。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 实用工具](../integration-services/dtutil-utility.md)|用于管理 SSIS 包。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[使用部署实用工具部署模型解决方案](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|用于将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[mssql 脚本编写器 （公共预览版）](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|用于 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库中生成的数据库对象的创建和插入的 T-SQL 脚本。|请参阅我们[GitHub 存储库](https://github.com/Microsoft/sql-xplat-cli)有关下载和使用情况信息。| 
|[osql 实用工具](../tools/osql-utility.md)|您可以在命令提示符下输入 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句、系统过程和脚本文件。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler 实用工具](../tools/profiler-utility.md)|用于在命令提示符下启动 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 实用工具 (SSRS)](../reporting-services/tools/rs-exe-utility-ssrs.md)|用于运行专门管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器的脚本。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 实用工具 (SSRS)](../reporting-services/tools/rsconfig-utility-ssrs.md)|用于配置报表服务器连接。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 实用工具 (SSRS)](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|用于管理报表服务器上的加密密钥。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 应用程序](../tools/sqlagent90-application.md)|用于在命令提示符下启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理。|\<驱动器 >: files\microsoft SQL Server\\<*instance_name*> \MSSQL\Binn|  
|[sqlcmd Utility](../tools/sqlcmd-utility.md)|您可以在命令提示符下输入 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句、系统过程和脚本文件。|\<*驱动器*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 实用工具](../tools/sqldiag-utility.md)|用于为 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客户服务和支持部门收集诊断信息。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 应用程序](../tools/sqllogship-application.md)|应用程序可用其执行日志传送配置中的备份、复制和还原操作以及相关的清除任务，而无需运行备份、复制和还原作业。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 实用工具](../tools/sqllocaldb-utility.md)|针对程序开发人员的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的执行模式。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[sqlmaint 实用工具](../tools/sqlmaint-utility.md)|用于执行在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中创建的数据库维护计划。|\<驱动器 >: files\microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\Binn|  
|[sqlps 实用工具](../tools/sqlps-utility.md)|用于运行 PowerShell 命令和脚本。 加载和注册 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供程序和 cmdlet。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr Application](../tools/sqlservr-application.md)|用于在命令提示符下启动和停止 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例以进行故障排除。|\<驱动器 >: files\microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\Binn|  
|[Ssms 实用工具](../tools/sql-server-management-studio/ssms-utility.md)|用于在命令提示符下启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 实用工具](../tools/tablediff-utility.md)|用于比较两个表中的数据以查看数据是否无法收敛，这对于排除复制拓扑故障很有用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>SQL 命令提示实用工具语法约定  
  
|**约定**|**用于**|  
|--------------------|------------------|  
|大写|在操作系统层使用的语句和术语。|  
|`monospace`|示例命令和程序代码。|  
|*斜体*|用户提供的参数。|  
|**粗体**|命令、参数和其他必须严格按所给形式键入的语法。|  


