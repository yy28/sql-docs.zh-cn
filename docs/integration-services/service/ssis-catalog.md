---
title: "SSIS 目录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# SSIS 目录
  **SSISDB** 目录是使用已部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 项目的中心点。 例如，您可以设置项目和包参数，配置环境以便为包指定运行时值，执行包并对包进行故障排除，以及管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器操作。  
  
 **SSISDB** 目录中存储的对象包括项目、包、参数、环境和操作历史记录。  
  
 可通过查询 **“SSISDB”** 数据库中的视图来检查 **“SSISDB”** 目录中存储的对象、设置和操作数据。 可通过调用 **SSISDB** 数据库中的存储过程或通过使用 **SSISDB** 目录的 UI 来管理对象。 在很多情况下，同一个任务既可使用 UI 执行，也可以通过调用存储过程来执行。  
  
 要维护 **SSISDB** 数据库，建议您应用管理用户数据库的标准企业策略。 有关创建维护计划的信息，请参阅 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)。  
  
 **SSISDB** 目录和 **SSISDB** 数据库支持 Windows PowerShell。 有关将 SQL Server 与 Windows PowerShell 一起使用的详细信息，请参阅 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)。 有关如何使用 Windows PowerShell 完成任务（如部署项目）的示例，请参阅 blogs.msdn.com 上的博客文章 [SQL Server 2012 中的 SSIS 和 PowerShell](http://go.microsoft.com/fwlink/?LinkId=242539)。  
  
 有关如何查看操作数据的详细信息，请参阅 [监视运行包和其他操作](../../integration-services/performance/monitor-running-packages-and-other-operations.md)。  
  
 您可以通过以下方式访问 **中的** “SSISDB” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 目录：连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎，然后展开对象资源管理器中的 **“Integration Services 目录”** 节点。 可通过展开对象资源管理器中的“数据库”节点来访问 **中的** SSISDB [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 数据库。  
  
> [!NOTE] 不能重命名 **SSISDB** 数据库。  
  
> [!NOTE] 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSISDB **数据库附加到的** 实例停止或不响应，则 ISServerExec.exe 进程结束。 向 Windows 事件日志写入一条消息。  
>   
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 资源作为群集故障转移的一部分进行故障转移，则正在运行的包不重新启动。 您可以使用检查点来重新启动包。 有关详细信息，请参阅 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
## <a name="in-this-topic"></a>本主题内容  
  
-   [目录对象标识符](../../integration-services/service/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [目录配置](../../integration-services/service/ssis-catalog.md#Configuration)  
  
-   [权限](../../integration-services/service/ssis-catalog.md#Permissions)  
  
-   [文件夹](../../integration-services/service/ssis-catalog.md#Folders)  
  
-   [项目和包](../../integration-services/service/ssis-catalog.md#ProjectsAndPackages)  
  
-   [参数](../../integration-services/service/ssis-catalog.md#Parameters)  
  
-   [服务器环境、服务器变量和服务器环境引用](../../integration-services/service/ssis-catalog.md#ServerEnvironments)  
  
-   [执行和验证](../../integration-services/service/ssis-catalog.md#Executions)  
  
-   [AlwaysOn 支持](../../integration-services/service/ssis-catalog.md#AlwaysOn)  
  
-   [相关任务](../../integration-services/service/ssis-catalog.md#RelatedTasks)  
  
-   [相关内容](../../integration-services/service/ssis-catalog.md#RelatedContent)  
  
##  <a name="a-namecatalogobjectidentifiersa-catalog-object-identifiers"></a><a name="CatalogObjectIdentifiers"></a>目录对象标识符  
 在目录中创建新对象时，为该对象指定一个名称。 对象名称就是一个标识符。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定义了有关可在标识符中使用的字符的规则。 以下对象的名称必须遵循标识符规则。  
  
-   文件夹  
  
-   项目  
  
-   环境  
  
-   参数  
  
-   环境变量  
  
###  <a name="a-namefoldera-folder-project-environment"></a><a name="Folder"></a>文件夹、项目和环境  
 重命名文件夹、项目或环境时，请考虑以下规则。  
  
-   无效字符包括 ASCII/Unicode 字符 1 到 31、引号 (")、小于号 (\<)、大于号 (>)、竖线 (|)、退格符 (\b)、null (\0) 和制表符 (\t)。  
  
-   名称不得包含前导空格或尾随空格。  
  
-   不允许将 @ 作为第一个字符，但后续字符可使用 @.  
  
-   名称的长度必须大于 0 且小于或等于 128。  
  
###  <a name="a-nameparametera-parameter"></a><a name="Parameter"></a>参数  
 命名参数时，请考虑以下规则。  
  
-   名称的第一个字符必须是在 Unicode 标准 2.0 中定义的字母，或者是下划线 (_)。  
  
-   后续字符可以是在 Unicode 标准 2.0 中定义的字母或数字，或是下划线 (_)。  
  
###  <a name="a-nameenvironmentvariablea-environment-variable"></a><a name="EnvironmentVariable"></a>环境变量  
 命名环境变量时，请考虑以下规则。  
  
-   无效字符包括 ASCII/Unicode 字符 1 到 31、引号 (")、小于号 (\<)、大于号 (>)、竖线 (|)、退格符 (\b)、null (\0) 和制表符 (\t)。  
  
-   名称不得包含前导空格或尾随空格。  
  
-   不允许将 @ 作为第一个字符，但后续字符可使用 @.  
  
-   名称的长度必须大于 0 且小于或等于 128。  
  
-   名称的第一个字符必须是在 Unicode 标准 2.0 中定义的字母，或者是下划线 (_)。  
  
-   后续字符可以是在 Unicode 标准 2.0 中定义的字母或数字，或是下划线 (_)。  
  
##  <a name="a-nameconfigurationa-catalog-configuration"></a><a name="Configuration"></a>目录配置  
 通过调整目录属性来优化目录的行为方式。 目录属性定义如何对敏感数据进行加密，以及如何保留操作和项目版本控制数据。 若要设置目录属性，请使用“目录属性”对话框，或调用 [catalog.configure_catalog（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)存储过程。 若要查看属性，请使用对话框或查询 [catalog.catalog_properties（SSISDB 数据库）](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)。 可以通过右键单击对象资源管理器中的 **SSISDB** 来访问该对话框。  
  
###  <a name="a-namecleanupa-operations-and-project-version-cleanup"></a><a name="Cleanup"></a>操作和项目版本清理  
 目录中很多操作的状态数据都存储在内部数据库表中。 例如，目录会跟踪包执行和项目部署的状态。 为了维持操作数据的大小，使用 **中的** “SSIS Server 维护作业” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来删除旧数据。 在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时创建此 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 代理作业。  
  
 您可以使用相同名称将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目部署到目录中的同一文件夹，以对其进行更新或重新部署。 默认情况下，每次重新部署某个项目时， **SSISDB** 目录都会保留早期版本的该项目。 为了维持操作数据的大小，使用了 **“SSIS 服务器维护作业”** 来删除旧版本的项目。  
 
为了运行“SSIS 服务器维护作业”，SSIS 创建了 SQL Server 登录 **##MS_SSISServerCleanupJobLogin##**。 此登录仅供 SSIS 进行内部使用。
  
 以下 **SSISDB** 目录属性将定义此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的行为方式。 可以使用“目录属性”对话框或使用 [catalog.catalog_properties（SSISDB 数据库）](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)和 [catalog.configure_catalog（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)查看和修改属性。  
  
 **定期清理日志**  
 当此属性设置为 **True**时，操作清除作业步骤将会运行。  
  
 **保持期(天)**  
 定义可允许的操作数据的最长保存时间（以天为单位）。 将删除较旧的数据。  
  
 最小值为一天。 最大值仅受到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** 数据的最大值的限制。 有关此数据类型的信息，请参阅 [int、bigint、smallint 和 tinyint (Transact-SQL)](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)。  
  
 **定期删除旧版本**  
 当此属性设置为 **True**时，项目版本清除作业步骤将会运行。  
  
 **每个项目的最大版本数**  
 定义在目录中存储项目的多少个版本。 将删除较旧版本的项目。  
  
###  <a name="a-nameencryptiona-encryption-algorithm"></a><a name="Encryption"></a>加密算法  
 **“加密算法”** 属性可指定用于对敏感参数值进行加密的加密类型。 可以从下列加密类型中选择。  
  
-   AES_256（默认值）  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 在向 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器部署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]项目时，该目录会自动对包数据和敏感值加密。 该目录还会在检索数据时自动解密数据。 SSISDB 目录使用 **ServerStorage** 保护级别。 有关详细信息，请参阅 [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)。  
  
 更改加密算法是一项很耗时的操作。 首先，服务器必须使用以前指定的算法来解密所有配置值。 然后，服务器必须使用新算法来重新对这些值进行加密。 此时，在服务器上不能有其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作。 因此，为使 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 操作继续运行而不会中断，加密算法在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的对话框中是只读值。  
  
 若要更改 **“加密算法”** 属性设置，请将 **“SSISDB”** 数据库设置为单用户模式，然后调用 catalog.configure_catalog 存储过程。 将 ENCRYPTION_ALGORITHM 用于 *property_name* 参数。 有关支持的属性值，请参阅 [catalog.catalog_properties（SSISDB 数据库）](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)。 有关该存储过程的详细信息，请参阅 [catalog.configure_catalog（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)。  
  
 有关单用户模式的详细信息，请参阅[将数据库设置为单用户模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中加密和加密算法的信息，请参阅 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)一节中的有关主题。  
  
 数据库主密钥用于加密。 创建目录时会创建此密钥。 有关详细信息，请参阅 [创建 SSIS 目录](../../integration-services/service/create-the-ssis-catalog.md)。  
  
 下表列出了 **“目录属性”** 对话框中显示的属性名称和数据库视图中对应的属性。  
  
|属性名称（**“目录属性”** 对话框）|属性名称（数据库视图）|  
|---------------------------------------------------------|-------------------------------------|  
|加密算法名称|ENCRYPTION_ALGORITHM|  
|定期清理日志|OPERATION_CLEANUP_ENABLED|  
|保持期(天)|RETENTION_WINDOW|  
|定期删除旧版本|VERSION_CLEANUP_ENABLED|  
|每个项目的最大版本数|MAX_PROJECT_VERSIONS|  
|服务器范围的默认日志记录级别|SERVER_LOGGING_LEVEL|  
  
##  <a name="a-namepermissionsa-permissions"></a><a name="Permissions"></a>权限  
 文件夹中包含的项目、环境和包是安全对象。 您可以授予对文件夹的权限，包括 MANAGE_OBJECT_PERMISSIONS 权限。 利用 MANAGE_OBJECT_PERMISSIONS，您可以将文件夹内容的管理委托给用户，而无需为 ssis_admin 角色授予用户成员身份。 您还可以授予对项目、环境和操作的权限。 操作包括初始化 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、部署项目、创建和启动执行、验证项目和包以及配置 **SSISDB** 目录。  
  
 有关数据库角色的详细信息，请参阅 [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
 SSISDB 目录使用 DDL 触发器 (ddl_cleanup_object_permissions) 强制 SSIS 安全对象的权限信息的完整性。 当从 SSISDB 数据库中删除数据库主体（如数据库用户、数据库角色或数据库应用程序角色）时，将会触发触发器。  
  
 如果该主体已对其他主体授予或拒绝权限，则应先撤消授权者授予的权限，然后才能删除主体。 否则，系统尝试删除主体时会返回一条错误消息。 触发器将删除数据库主体作为被授权者的所有权限记录。  
  
 建议不要禁用触发器，因为它可确保在从 **SSISDB** 数据库中删除数据库主体之后，不会出现孤立的权限记录。  
  
### <a name="managing-permissions"></a>管理权限  
 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用户界面、存储过程以及 <xref:Microsoft.SqlServer.Management.IntegrationServices> 命名空间来管理权限。  
  
 若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用户界面管理权限，请使用下面的对话框。  
  
-   对于一个文件夹中，使用 **权限** 页 [Folder Properties Dialog Box](../../integration-services/service/folder-properties-dialog-box.md)。  
  
-   对于项目，使用 **权限** 页 [Project Properties Dialog Box](../../integration-services/service/project-properties-dialog-box.md)。  
  
-   对于环境中，使用 **权限** 页 [NIB：环境属性](http://msdn.microsoft.com/zh-cn/6a91a8d4-0006-4cfd-9759-3e4295ae452b)。  
  
 若要使用 Transact-SQL 管理权限，请调用 [catalog.grant_permission（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)、[catalog.deny_permission（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md) and [catalog.revoke_permission（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)。 若要查看所有对象的当前主体的有效权限，请查询 [catalog.effective_object_permissions（SSISDB 数据库）](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)。 本主题描述了不同类型的权限。 若要查看已显式分配给用户的权限，请查询 [catalog.explicit_object_permissions（SSISDB 数据库）](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)。  
  
##  <a name="a-namefoldersa-folders"></a><a name="Folders"></a>文件夹  
 文件夹包含 **SSISDB** 目录中的一个或多个项目和环境。 可以使用 [catalog.folders（SSISDB 数据库）](../../integration-services/system-views/catalog-folders-ssisdb-database.md) 视图来访问有关目录中的文件夹的信息。 您可以使用以下存储过程管理文件夹。  
  
-   [catalog.create_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="a-nameprojectsandpackagesa-projects-and-packages"></a><a name="ProjectsAndPackages"></a>项目和包  
 每个项目可以包含多个包。 项目和包都可以包含参数和对环境的引用。 您可以使用 [Configure Dialog Box](../../integration-services/service/configure-dialog-box.md)访问参数和环境引用。  
  
 您可以通过调用以下存储过程执行其他项目任务。  
  
-   [catalog.delete_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
  
-   [catalog.restore_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 以下视图提供了有关包、项目和项目版本的详细信息。  
  
-   [catalog.projects（SSISDB 数据库）](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages（SSISDB 数据库）](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions（SSISDB 数据库）](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="a-nameparametersa-parameters"></a><a name="Parameters"></a>参数  
 您可以使用参数在包执行时为包属性赋值。 若要设置包或项目参数的值和清除这些值，请调用 [catalog.set_object_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)和 [catalog.clear_object_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)。 若要为执行实例设置参数的值，请调用 [catalog.set_execution_parameter_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)。 可以通过调用 [catalog.get_parameter_values（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)来检索默认参数值。  
  
 以下视图显示了所有包和项目的参数，以及用于执行实例的参数值。  
  
-   [catalog.object_parameters（SSISDB 数据库）](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values（SSISDB 数据库）](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="a-nameserverenvironmentsa-server-environments-server-variables-and-server-environment-references"></a><a name="ServerEnvironments"></a>服务器环境、服务器变量和服务器环境引用  
 服务器环境包含服务器变量。 当在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上执行或验证包时，可以使用这些变量值。  
  
 利用以下存储过程，您可以为环境和变量执行很多其他管理任务。  
  
-   [catalog.create_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
  
-   [catalog.delete_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
  
-   [catalog.move_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
  
-   [catalog.rename_environment（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
  
-   [catalog.set_environment_property（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
  
-   [catalog.create_environment_variable（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
  
-   [catalog.delete_environment_variable（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_property（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_value（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
  
 通过调用 [catalog.set_environment_variable_protection（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)存储过程，可以设置变量的敏感性位。  
  
 若要使用服务器变量的值，请指定项目和服务器环境之间的引用。 您可以使用以下存储过程创建和删除引用。 还可以指示环境是可以位于与项目相同的文件夹中，还是位于其他文件夹中。  
  
-   [catalog.create_environment_reference（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
  
-   [catalog.delete_environment_reference（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
  
-   [catalog.set_environment_reference_type（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
  
 有关环境和变量的详细信息，请查询以下视图。  
  
-   [catalog.environments（SSISDB 数据库）](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
  
-   [catalog.environment_variables（SSISDB 数据库）](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
  
-   [catalog.environment_references（SSISDB 数据库）](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
  
##  <a name="a-nameexecutionsa-executions-and-validations"></a><a name="Executions"></a>执行和验证  
 执行就是一个包执行实例。 调用 [catalog.create_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)和 [catalog.start_execution（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)可创建并启动执行。 若要停止执行或停止包/项目验证，请调用 [catalog.stop_operation（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)。  
  
 若要暂停正在运行的包和创建转储文件，请调用 catalog.create_execution_dump 存储过程。 转储文件提供了有关包执行的信息，可帮助您解决执行问题。 有关生成和配置转储文件的详细信息，请参阅 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)。  
  
 有关执行、验证、操作期间记录的消息以及与错误有关的上下文信息的详细信息，请查询以下视图。  
  
-   [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
-   [catalog.operations（SSISDB 数据库）](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
  
-   [catalog.operation_messages（SSISDB 数据库）](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
  
-   [catalog.extended_operation_info（SSISDB 数据库）](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
  
-   [catalog.event_messages](../../integration-services/system-views/catalog-event-messages.md)  
  
-   [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
 可以通过调用 [catalog.validate_project（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)和 [catalog.validate_package（SSISDB 数据库）](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)存储过程验证项目和包。 [catalog.validations（SSISDB 数据库）](../../integration-services/system-views/catalog-validations-ssisdb-database.md)视图提供了有关验证的详细信息，例如，验证中要考虑的服务器环境引用、验证是依赖项验证还是完整验证以及使用 32 位运行时还是 64 位运行时来运行包。  
  
##  <a name="a-namealwaysona-alwayson-support"></a><a name="AlwaysOn"></a>AlwaysOn 支持  
 AlwaysOn 可用性组功能是一个高可用性和灾难恢复解决方案，可以提供替代数据库镜像的企业级方案。 可用性组针对一组离散的用户数据库（称为可用性数据库，它们共同实现故障转移）支持故障转移环境。 有关详细信息，请参阅 [AlwaysOn 可用性组](https://msdn.microsoft.com/library/hh510230.aspx)。  
  
 SQL Server Integration Services (SSIS) 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中引入了新功能，你可以轻松地将其部署到集中式 SSIS 目录（即 SSISDB 用户数据库）。 为了对 SSISDB 数据库及其内容（项目、包、执行日志等）提供高可用性，可以将 SSISDB 数据库（与其他任何用户数据库相同）添加到 AlwaysOn 可用性组。 当发生故障转移时，其中一个辅助节点将自动成为新的主节点。  
  
 有关如何为 SSISDB 启用 AlwaysOn 的详细概述和分步说明，请参阅 [SSIS 目录 (SSISDB) 的 AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md)。  
  
##  <a name="a-namerelatedtasksa-related-tasks"></a><a name="RelatedTasks"></a>相关任务  
  
-   [创建 SSIS 目录](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [备份、还原和移动 SSIS 目录](../../integration-services/service/backup-restore-and-move-the-ssis-catalog.md)  
  
##  <a name="a-namerelatedcontenta-related-content"></a><a name="RelatedContent"></a>相关内容  
  
-   blogs.msdn.com 上的博客文章 [SQL Server 2012 中的 SSIS 和 PowerShell](http://go.microsoft.com/fwlink/?LinkId=242539)。  
  
-   blogs.msdn.com 上的博客文章 [SSIS 目录访问控制提示](http://go.microsoft.com/fwlink/?LinkId=246669)。  
  
-   blogs.msdn.com 上的博客文章： [SSIS 目录托管对象模型一瞥](http://go.microsoft.com/fwlink/?LinkId=254267)。  
  
  