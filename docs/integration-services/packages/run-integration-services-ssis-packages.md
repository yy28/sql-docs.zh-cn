---
title: 运行 Integration Services (SSIS) 包 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b46ed84db9ad5339639119a8d5f29644c7be8fc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757335"
---
# <a name="run-integration-services-ssis-packages"></a>运行 Integration Services (SSIS) 包
  要运行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包，您可以根据包的存储位置使用某个工具。 下表中列出了这些工具。  

> [!NOTE]
> 本文介绍如何在一般情况下运行 SSIS 包以及如何在本地运行包。 还可在以下平台上运行 SSIS 包：
> - **Microsoft Azure 云**。 有关详细信息，请参阅[将 SQL Server Integration Services 工作负荷直接迁移到云](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)和[在 Azure 中运行 SSIS 包](../lift-shift/ssis-azure-run-packages.md)。
> - **Linux**。 有关详细信息，请参阅[使用 SSIS 在 Linux 上提取、转换和加载数据](../../linux/sql-server-linux-migrate-ssis.md)。
  
 为了在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上存储包，您使用项目部署模型将项目部署到服务器。 有关信息，请参阅[部署 Integration Services (SSIS) 项目和包](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 为了在 SSIS 包存储区、msdb 数据库或文件系统中存储包，您使用包部署模型。 有关详细信息，请参阅[早期包部署 (SSIS)](../../integration-services/packages/legacy-package-deployment-ssis.md)。  
  
|工具|在 Integration Services 服务器上存储的包|在 SSIS 包存储区或 msdb 数据库中存储的包|在文件系统中存储的包，在属于 SSIS 包存储区的位置之外|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|否|否<br /><br /> 但是，你可以将现有包从包括 msdb 数据库的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区添加到项目中。 以此方式将现有包添加到项目中将在文件系统中生成该包的本地副本。|用户帐户控制|  
|**SQL Server Management Studio（连接到托管 Integration Services 服务器的数据库引擎实例时）**<br /><br /> 有关详细信息，请参阅 [Execute Package Dialog Box](#execute_package_dialog)|用户帐户控制|否<br /><br /> 但是，可以从这些位置将包导入服务器。|否<br /><br /> 但是，可以从文件系统将包导入服务器。|
|**SQL Server Management Studio（连接到托管启用为 Scale Out Master 的 Integration Services 服务器的数据库引擎实例时）**<br /><br /> 有关详细信息，请参阅[在 Scale Out 中运行包](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)|用户帐户控制|否|否|
|**SQL Server Management Studio（连接到管理 SSIS 包存储的 Integration Services 服务时）**|否|是|否<br /><br /> 但是，可以从文件系统将包导入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包存储区中。|  
|**dtexec**<br /><br /> 有关详细信息，请参阅 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。|用户帐户控制|是|用户帐户控制|  
|**dtexecui**<br /><br /> 有关详细信息，请参阅[执行包实用工具 (DtExecUI) 用户界面参考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|否|是|用户帐户控制|  
|**SQL Server 代理**<br /><br /> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业计划运行包。<br /><br /> 有关详细信息，请参阅 [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)。|用户帐户控制|是|用户帐户控制|  
|**内置存储过程**<br /><br /> 有关详细信息，请参阅 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|用户帐户控制|否|否|  
|**托管的 API，通过使用** <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间中的类型和成员|用户帐户控制|否|否|  
|**托管的 API，通过使用** <xref:Microsoft.SqlServer.Dts.Runtime> 命名空间中的类型和成员|目前不可用|用户帐户控制|用户帐户控制|  

## <a name="execution-and-logging"></a>执行和日志记录  
 可以启用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包进行日志记录，这样就可以在日志文件中捕获运行时信息。 有关详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
 您可以使用操作报告监视部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器并在其上运行的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用这些报告。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中运行包
  在开发、调试和测试包的过程中，通常在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中运行包。 在从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器运行包时，包始终可以立即运行。  
  
 包运行时， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器在 **“进度”** 选项卡上显示包执行的进度。除了有关包中失败的所有任务或容器的信息外，还可以查看包及其任务和容器的开始时间和完成时间。 在包完成运行后，运行时信息仍显示在“执行结果”选项卡上。有关详细信息，请参阅 [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)主题中的“进度报告”部分。  
  
 **设计时部署**。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中运行包时，包被生成，然后部署到文件夹。 在运行包前，可以指定要包将部署到其中的文件夹。 如果未指定文件夹，默认将使用 **bin** 文件夹。 这种部署称为设计时部署。  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中运行包  
  
1.  在“解决方案资源管理器”中，如果解决方案包含多个项目，则右键单击包含包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目，然后单击“设为启动对象”以便设置启动项目。  
  
2.  在“解决方案资源管理器”中，如果项目包含多个包，则右键单击某个包，然后单击“设为启动对象”以便设置启动包。  
  
3.  若要运行包，请执行以下操作：  
  
    -   打开要运行的包，然后单击菜单栏上的 **“启动调试”** ，或按 F5。 包运行完成后，按 Shift+F5 返回设计模式。  
  
    -   在“解决方案资源管理器”中，右键单击包，然后单击“执行包”。  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>为设计时部署指定不同文件夹  
  
1.  在“解决方案资源管理器”中，右键单击包含要运行的包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目文件夹，然后单击“属性”。  
  
2.  在“\<项目名称> 属性页”对话框中，单击“生成”。  
  
3.  更新 OutputPath 属性中的值以指定要用于设计时部署的文件夹，然后单击“确定”。  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在 SSIS 服务器上运行包
  在将您的项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器中之后，可以在该服务器上运行此包。  
  
 您可以使用操作报告查看有关服务器上已运行或当前正在运行的包的信息。 有关详细信息，请参阅 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)。  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在服务器上运行包  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并连接到包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目录的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中，展开 **“Integration Services 目录”** 节点，再展开 **“SSISDB”** 节点，然后导航到包含在您部署的项目中的包。  
  
3.  右键单击包名称，然后选择“执行”。  
  
4.  使用 **“执行包”** 对话框中的 **“参数”**、 **“连接管理器”** 和 **“高级”** 选项卡上的设置来配置包执行。  
  
5.  单击 **“确定”** 运行包。  
  
     -或 -  
  
     使用存储过程来运行包。 单击“脚本”生成创建执行实例并启动执行实例的 Transact-SQL 语句。 该语句包含对 catalog.create_execution、catalog.set_execution_parameter_value 和 catalog.start_execution 存储过程的调用。 有关这些存储过程的详细信息，请参阅 [catalog.create_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)和 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。  

## <a name="execute_package_dialog"></a> Execute Package Dialog Box
  使用 **“执行包”** 对话框可以运行在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上存储的包。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包可以包含在环境变量中存储的值的参数。 在执行此类包之前，您必须指定将使用哪一环境来提供环境变量值。 一个项目可以包含多个环境，但只能使用一个环境在执行时绑定环境变量值。 如果在包中未使用任何环境变量，则不要求环境。  
  
 您希望做什么？  
  
-   [打开“执行包”对话框](#open_dialog)  
  
-   [设置“常规”页上的选项](#general)  
  
-   [设置“参数”选项卡上的选项](#parameters)  
  
-   [设置“连接管理器”选项卡上的选项](#connection)  
  
-   [设置“高级”选项卡上的选项](#advanced)  
  
-   [编写“执行包”对话框中选项的脚本](#script)  
  
###  <a name="open_dialog"></a> 打开“执行包”对话框  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器。  
  
     您在连接到承载 SSISDB 数据库的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例。  
  
2.  在对象资源管理器中，展开树以便显示 **“Integration Services 目录”** 节点。  
  
3.  展开 **“SSISDB”** 节点。  
  
4.  展开包含您要运行的包的文件夹。  
  
5.  右键单击该包，然后单击“执行”。  
  
###  <a name="general"></a> 设置“常规”页上的选项  
 选择 **“环境”** 以便指定适用于运行的包的环境。  
  
###  <a name="parameters"></a> 设置“参数”选项卡上的选项  
 使用 **“参数”** 选项卡可以修改在包运行时使用的参数值。  
  
###  <a name="connection"></a> 设置“连接管理器”选项卡上的选项  
 使用“连接管理器”选项卡可以设置包连接管理器的属性。  
  
###  <a name="advanced"></a> 设置“高级”选项卡上的选项  
 使用“高级”选项卡可以管理属性和其他包设置。  
  
 “添加”、“编辑”、“删除”  
 单击以便添加、编辑或删除某一属性。  
  
 **日志记录级别**  
 选择用于执行包的日志记录级别。 有关详细信息，请参阅 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)。  
  
 **出错时转储**  
 指定在包执行过程中发生错误时是否创建一个转储文件。 有关详细信息，请参阅 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。  
  
 **32 位运行时**  
 指定包将在 32 位系统上执行。  
  
###  <a name="script"></a> 编写“执行包”对话框中选项的脚本  
 在您处于 **“执行包”** 对话框中时，还可以使用工具栏上的 **“脚本”** 按钮为您编写 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码。 生成的脚本使用与你在“执行包”对话框中选择的相同选项调用存储过程 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。 该脚本出现在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的新脚本窗口中。  

## <a name="see-also"></a>另请参阅  
 [dtexec 实用工具](../../integration-services/packages/dtexec-utility.md)   
[启动 SQL Server 导入和导出向导](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
