---
title: 命令提示实用工具参考（数据库引擎） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfb77db3676c8df124b65199fb0b806755e550a1
ms.sourcegitcommit: b4962530f90234017073b3fdd2248936b2de4e69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71077514"
---
# <a name="command-prompt-utility-reference-database-engine"></a>命令提示实用工具参考（数据库引擎）
  使用命令提示实用工具，可以编写 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 操作的脚本。 下表包含了随 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供的命令提示实用工具列表。  
  
|**实用工具**|**说明**|**安装位置**|  
|-----------------|---------------------|----------------------|  
|[bcp 实用工具](bcp-utility.md)|用于在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例和用户指定格式的数据文件之间复制数据。|\<驱动器:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 实用工具](dta/dta-utility.md)|用于分析工作负荷并建议物理设计结构，以优化该工作负荷下的服务器性能。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 实用工具](../integration-services/packages/dtexec-utility.md)|用于配置和执行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。 该命令提示实用工具的用户界面版本称为 **DTExecUI**，它可提供执行包实用工具。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 实用工具](../integration-services/dtutil-utility.md)|用于管理 SSIS 包。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[使用部署实用工具部署模型解决方案](https://docs.microsoft.com/analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility)|用于将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[osql 实用工具](osql-utility.md)|您可以在命令提示符下输入 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句、系统过程和脚本文件。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler 实用工具](profiler-utility.md)|用于在命令提示符下启动 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 实用工具 (SSRS)](../reporting-services/tools/rs-exe-utility-ssrs.md)|用于运行专门管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表服务器的脚本。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 实用工具 (SSRS)](../reporting-services/tools/rsconfig-utility-ssrs.md)|用于配置报表服务器连接。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 实用工具 (SSRS)](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|用于管理报表服务器上的加密密钥。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 应用程序](sqlagent90-application.md)|用于在命令提示符下启动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理。|\<驱动器>:\Program Files\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd Utility](sqlcmd-utility.md)|您可以在命令提示符下输入 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句、系统过程和脚本文件。|\<驱动器:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 实用工具](sqldiag-utility.md)|用于为 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客户服务和支持部门收集诊断信息。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 应用程序](sqllogship-application.md)|应用程序可用其执行日志传送配置中的备份、复制和还原操作以及相关的清除任务，而无需运行备份、复制和还原作业。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 实用工具](sqllocaldb-utility.md)|针对程序开发人员的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的执行模式。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 实用工具](sqlmaint-utility.md)|用于执行在早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中创建的数据库维护计划。|\<drive>:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 实用工具](sqlps-utility.md)|用于运行 PowerShell 命令和脚本。 加载和注册 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供程序和 cmdlet。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr Application](sqlservr-application.md)|用于在命令提示符下启动和停止 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例以进行故障排除。|\<drive>:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
|[Ssms 实用工具](../ssms/ssms-utility.md)|用于在命令提示符下启动 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 实用工具](tablediff-utility.md)|用于比较两个表中的数据以查看数据是否无法收敛，这对于排除复制拓扑故障很有用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  
  
 **使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 访问 [!INCLUDE[win8](../includes/win8-md.md)]**  
  
 因为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以，当运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 时， [!INCLUDE[win8](../includes/win8-md.md)]配置管理器不显示为一个应用程序。 要打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器，请在“搜索”超级按钮中的“应用”下，键入 **SQLServerManager12.msc**（对于 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]）或 **SQLServerManager11.msc**（对于 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]），然后按“Enter”键。  
  
## <a name="command-prompt-utilities-syntax-conventions"></a>命令提示实用工具语法约定  
  
|**约定**|**用于**|  
|--------------------|------------------|  
|大写|在操作系统层使用的语句和术语。|  
|`monospace`|示例命令和程序代码。|  
|*斜体*|用户提供的参数。|  
|**粗体**|命令、参数和其他必须严格按所给形式键入的语法。|  
  
## <a name="see-also"></a>请参阅  
 [复制分发代理](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [复制日志读取器代理](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [复制合并代理](../relational-databases/replication/agents/replication-merge-agent.md)   
 [复制队列读取器代理](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [复制快照代理](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
