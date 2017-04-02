---
title: "运行 Integration Services (SSIS) 包 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 包, 运行"
  - "SSIS 包, 运行"
  - "包 [Integration Services], 运行"
  - "SQL Server Integration Services 包, 运行"
  - "执行包 [Integration Services]"
  - "正在运行的包 [Integration Services]"
  - "Integration Services,（请参阅 Integration Services 包）"
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# 运行 Integration Services (SSIS) 包
  要运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，您可以根据包的存储位置使用某个工具。 下表中列出了这些工具。  
  
 为了在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上存储包，您使用项目部署模型将项目部署到服务器。 有关信息，请参阅 [Deploy Projects to Integration Services Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md)。  
  
 为了在 SSIS 包存储区、msdb 数据库或文件系统中存储包，您使用包部署模型。 有关详细信息，请参阅[早期包部署 (SSIS)](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
|工具|在 Integration Services 服务器上存储的包|在 SSIS 包存储区或 msdb 数据库中存储的包|在文件系统中存储的包，在属于 SSIS 包存储区的位置之外|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|“否”|“否”<br /><br /> 但是，你可以将现有包从包括 msdb 数据库的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区添加到项目中。 以此方式将现有包添加到项目中将在文件系统中生成该包的本地副本。|是|  
|**SQL Server Management Studio（连接到托管 Integration Services 服务器的数据库引擎实例时）**<br /><br /> 有关详细信息，请参阅 [Execute Package Dialog Box](../../integration-services/packages/execute-package-dialog-box.md)|是|“否”<br /><br /> 但是，可以从这些位置将包导入服务器。|“否”<br /><br /> 但是，可以从文件系统将包导入服务器。|
|**SQL Server Management Studio（连接到托管启用为 Scale Out Master 的 Integration Services 服务器的数据库引擎实例时）**<br /><br /> 有关详细信息，请参阅[在 Scale Out 中运行包](../../integration-services/run-packages-in-integration-services-ssis-scale-out.md)|是|是|“否”|
|**SQL Server Management Studio（连接到管理 SSIS 包存储的 Integration Services 服务时）**|“否”|是|“否”<br /><br /> 但是，可以从文件系统将包导入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中。|  
|**dtexec**<br /><br /> 有关详细信息，请参阅 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。|是|用户帐户控制|是|  
|**dtexecui**<br /><br /> 有关详细信息，请参阅[执行包实用工具 (DtExecUI) 用户界面参考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|“否”|用户帐户控制|是|  
|**SQL Server 代理**<br /><br /> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业计划运行包。<br /><br /> 有关详细信息，请参阅 [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。|是|用户帐户控制|是|  
|**内置存储过程**<br /><br /> 有关详细信息，请参阅 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|是|是|“否”|  
|**托管的 API，通过使用** <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间中的类型和成员|是|是|“否”|  
|**托管的 API，通过使用** <xref:Microsoft.SqlServer.Dts.Runtime> 命名空间中的类型和成员|目前不可用|是|是|  
  
## <a name="execution-and-logging"></a>执行和日志记录  
 可以启用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包进行日志记录，这样就可以在日志文件中捕获运行时信息。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 您可以使用操作报告监视部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器并在其上运行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用这些报告。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)。  
  
## <a name="related-tasks"></a>相关任务  
  
-   [使用 SQL Server 代理计划包](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
-   [在 SQL Server Data Tools 中运行包](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
-   [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [dtexec 实用工具](../../integration-services/packages/dtexec-utility.md)   
[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  