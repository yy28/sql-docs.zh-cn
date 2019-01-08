---
title: 部署和使用存储过程执行 SSIS 包 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5aee74a2b0bd632e2efcb780a52f1b05f1949669
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210936"
---
# <a name="deploy-and-execute-ssis-packages-using-stored-procedures"></a>使用存储过程部署和执行 SSIS 包
  在您配置一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目以便使用项目部署模型时，可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 目录中的存储过程部署该项目并且执行包。 有关项目部署模型的信息，请参阅 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
 您还可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 部署项目和执行包。 有关详细信息，请参阅“另请参见”  部分中的主题。  
  
> [!TIP]
>  您可以通过执行以下操作为下面的过程中列出的存储过程轻松地生成 Transact-SQL 语句，但 catalog.deploy_project 除外：  
> 
>  1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，在对象资源管理器中展开“Integration Services 目录”  节点，然后导航到您要执行的包。  
> 2.  右键单击该包，然后单击“执行”。  
> 3.  根据需要，设置参数值、连接管理器属性和 **“高级”** 选项卡中的选项（例如，日志记录级别）。  
> 
>      有关日志记录级别的详细信息，请参阅 [Enable Logging for Package Execution on the SSIS Server](../../2014/integration-services/enable-logging-for-package-execution-on-the-ssis-server.md)。  
> 4.  在单击 **“确定”** 以便执行该包之前，单击 **“脚本”**。 Transact-SQL 将出现在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的“查询编辑器”窗口中。  
  
## <a name="to-deploy-and-execute-a-package-using-stored-procedures"></a>使用存储过程部署和执行包  
  
1.  调用 [catalog.deploy_project（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database) 将包含包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器。  
  
     若要检索 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目部署文件的二进制内容，对于 *@project_stream* 参数，请将 SELECT 语句与 OPENROWSET 函数和 BULK 行集提供程序一起使用。 通过 BULK 行集提供程序，您可以从文件读取数据。 BULK 行集提供程序的 SINGLE_BLOB 参数将该数据文件的内容以 varbinary(max) 类型的单行、单列行集的形式返回。 有关详细信息，请参阅 [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql)。  
  
     在下面的示例中，SSISPackages_ProjectDeployment 项目将部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务器上的“SSIS 包”文件夹。 二进制数据从项目文件 (SSISPackage_ProjectDeployment.ispac) 读取并且存储于 varbinary(max) 类型的 *@ProjectBinary* 参数中。 将 *@ProjectBinary* 参数值赋给 *@project_stream* 参数。  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  调用 [catalog.create_execution（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) 来创建包执行的实例，并根据需要调用 [catalog.set_execution_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) 来设置运行时参数值。  
  
     在下面的示例中，catalog.create_execution 为在 SSISPackage_ProjectDeployment 项目中包含的 package.dtsx 创建一个执行实例。 该项目位于“SSIS 包”文件夹中。 存储过程返回的 execution_id 用于对 catalog.set_execution_parameter_value 的调用中。 此第二个存储过程将 LOGGING_LEVEL 参数设置为 3（详细日志记录），并且将名为 Parameter1 的包参数设置为值 1。  
  
     对于 LOGGING_LEVEL 之类的参数，object_type 值为 50。 对于包参数，object_type 值为 30。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  调用 [catalog.start_execution（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)执行包。  
  
     在下面的示例中，将对 catalog.start_execution 的调用添加到 Transact-SQL 以便开始包执行。 将使用 catalog.create_execution 存储过程返回的 execution_id。  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## <a name="to-deploy-a-project-from-server-to-server-using-stored-procedures"></a>使用存储过程将项目从一个服务器部署到另一个服务器  
 可以通过使用 [catalog.get_project（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)和 [catalog.deploy_project（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)存储过程在服务器之间部署项目。  
  
 在运行存储过程之前，您需要执行以下操作。  
  
-   创建一个链接服务器对象。 有关详细信息，请参阅[创建链接服务器（SQL Server 数据库引擎）](../database-engine/sql-server-database-engine-overview.md)。  
  
     在 **“链接服务器属性”** 的 **“服务器选项”** 页上，将 **RPC** 和 **RPC Out** 设置为 **True**。 此外，将 **“为 RPC 启用针对分布式事务的升级”** 设置为 **False**。  
  
-   通过在对象资源管理器中展开“链接服务器”下的“提供程序”节点，右键单击该提供程序，然后单击“属性”，对为链接服务器选择的提供程序启用动态参数。 选择 **“动态参数”** 旁边的 **“启用”**。  
  
-   确认分布式事务处理协调器 (DTC) 在两个服务器上均启动。  
  
 调用 catalog.get_project 以便返回该项目的二进制文件，然后调用 catalog.deploy_project。 将 catalog.get_project 返回的值插入 varbinary(max) 类型的表变量中。 链接服务器无法返回类型为 varbinary(max) 的结果。  
  
 在下面的示例中，catalog.get_project 为链接服务器上的 SSISPackages 项目返回二进制文件。 catalog.deploy_project 将该项目部署到本地服务器上名为 DestFolder 的文件夹中。  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## <a name="see-also"></a>请参阅  
 [将项目部署到 Integration Services 服务器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [在 SQL Server Data Tools 中运行包](../../2014/integration-services/run-a-package-in-sql-server-data-tools.md)   
 [使用 SQL Server Management Studio 在 SSIS 服务器上运行包](run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  
