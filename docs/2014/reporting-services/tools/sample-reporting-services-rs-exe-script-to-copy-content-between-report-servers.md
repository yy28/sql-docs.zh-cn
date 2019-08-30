---
title: 用于在报表服务器之间迁移内容的示例 Reporting Services rs-232c 脚本 |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d81bb03a-a89e-4fc1-a62b-886fb5338150
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c8434c0db2ca394ec3fbfbab3613b2ea69ac042d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153814"
---
# <a name="sample-reporting-services-rsexe-script-to-migrate-content-between-report-servers"></a>用于在报表服务器之间迁移内容的示例 Reporting Services rs.exe 脚本
  本主题包括并说明一个示例 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] RSS 脚本，该脚本使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] report server to another report server, using the **RS.exe** utility. 本机模式和 SharePoint 模式下，RS.exe 都随 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]一起安装。 脚本将 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 项（例如，报表和订阅）从一个服务器复制到另一个服务器。 该脚本支持 SharePoint 模式和本机模式报表服务器。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式 | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式|  
  
##  <a name="bkmk_top"></a>本主题内容:  
  
-   [下载 ssrs_migration.rss 脚本](#bkmk_download_script)  
  
-   [支持的方案](#bkmk_supported_scenarios)  
  
-   [脚本迁移的项和资源](#bkmk_what_is_migrated)  
  
-   [所需的权限](#bkmk_required_permissions)  
  
-   [如何使用该脚本](#bkmk_how_to_use_the_script)  
  
-   [参数说明](#bkmk_parameter_description)  
  
-   [更多示例](#bkmk_more_examples)  
  
    -   [本机模式报表服务器到本机模式报表服务器](#bkmk_native_2_native)  
  
    -   [本机模式到 SharePoint 模式-根站点](#bkmk_native_2_sharepoint_root)  
  
    -   [本机模式到 SharePoint 模式-"bi" 网站集](#bkmk_native_2_sharepoint_with_site)  
  
    -   [SharePoint 模式到 SharePoint 模式-"bi" 网站集](#bkmk_sharepoint_2_sharepoint)  
  
    -   [本机模式到本机模式-Azure 虚拟机](#bkmk_native_to_native_Azure_vm)  
  
    -   [SharePoint 模式-Azure 虚拟机上的本机模式服务器的 "bi" 网站集](#bkmk_sharepoint_site_to_native_Azure_vm)  
  
-   [验证](#bkmk_verification)  
  
-   [故障排除](#bkmk_troubleshoot)  
  
##  <a name="bkmk_download_script"></a> 下载 ssrs_migration.rss 脚本  
 从 CodePlex 站点 [Reporting Services RS.exe 脚本迁移内容](https://azuresql.codeplex.com/releases/view/115207) 将脚本下载到本地文件夹。 有关详细信息，请参阅本主题中的 [如何使用该脚本](#bkmk_how_to_use_the_script) 部分。  
  
##  <a name="bkmk_supported_scenarios"></a> 支持的方案  
 该脚本支持 SharePoint 模式和本机模式报表服务器。 该脚本支持以下报表服务器版本：  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]  
  
 该脚本可用于在相同模式或不同模式的报表服务器之间复制内容。 例如，可以运行该脚本以便将 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 本机模式报表服务器的内容复制到 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] SharePoint 模式报表服务器。 可以从安装了 RS.exe 的任何服务器运行该脚本。 例如，在以下部署中，您可以：  
  
-   在服务器 A **上** 运行 RS.exe 和脚本。  
  
-   将内容从 服务器 B  
  
-   复制到 服务器 C  
  
|服务器名称|报表服务器模式|  
|-----------------|------------------------|  
|服务器 A|本机|  
|服务器 B|SharePoint|  
|服务器 C|SharePoint|  
  
 有关使用 RS.exe 实用工具的详细信息，请参阅 [RS.exe 实用工具 (SSRS)](rs-exe-utility-ssrs.md)。  
  
###  <a name="bkmk_what_is_migrated"></a> 脚本迁移的项和资源  
 该脚本将不会覆盖同名的现有内容项。  如果该脚本在目标服务器上检测到名称与源服务器上相同的项，则这些单独的项将导致“失败”消息，但该脚本将继续运行。 下表列出该脚本可迁移到目标报表服务器模式的内容和资源的类型。  
  
|项|是否迁移|SharePoint|描述|  
|----------|--------------|----------------|-----------------|  
|密码|**是**|**是**|**不** 迁移密码。 在迁移内容项后，在目标服务器上更新凭据信息。 例如，具有已存储凭据的数据源。|  
|我的报表|**是**|**是**|本机模式“我的报表”功能基于单个用户登录名，因此，对于使用 -u 参数以外的参数运行 rss 脚本的用户，脚本服务无权访问其“我的报表”文件夹中的内容。 此外, "我的报表" 不是[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] sharepoint 模式的一项功能, 文件夹中的项不能复制到 sharepoint 环境。 因此, 此脚本不会复制源本机模式 Report Server 上 "我的报表" 文件夹中的报表项。 若要通过此脚本迁移 "我的报表" 文件夹中的内容, 请完成以下操作:<br /><br /> 1) 在报表管理器中创建新文件夹。 或者，您可为每个用户创建文件夹或子文件夹。<br /><br /> 2) 以 "我的报表" 内容的用户身份登录。<br /><br /> 3) 在报表管理器中, 单击**我的报表**文件夹。<br /><br /> 4) 单击该文件夹的**详细信息**视图。<br /><br /> 5) 选择要复制的每个报表。<br /><br /> 6) 单击报表管理器工具栏中的 "**移动**"。<br /><br /> 7) 选择所需的目标文件夹。<br /><br /> 8) 为每个用户重复步骤2-7。<br /><br /> 9) 运行该脚本。|  
|历史记录|**是**|**是**||  
|历史记录设置|是|是|将迁移历史记录设置，但不迁移历史记录详细信息。|  
|“计划”|是|是|若要迁移计划，在目标服务器上需运行 SQL Server 代理。 如果在目标服务器上未运行 SQL Server 代理，将会显示如下错误消息：<br /><br /> `Migrating schedules: 1 items found. Migrating schedule: theMondaySchedule ... FAILURE:  The SQL Agent service is not running. This operation requires the SQL Agent service. ---> Microsoft.ReportingServices.Diagnostics.Utilities.SchedulerNotResponding Exception: The SQL Agent service is not running. This operation requires the SQL Agent service.`|  
|角色和系统策略|是|是|默认情况下，该脚本不会在服务器之间复制自定义权限架构。 默认行为是将 "inherit parent 权限" 标志设置为 TRUE 的项将复制目标服务器。 如果您希望该脚本复制单独项的权限，请使用 SECURITY 开关。<br /><br /> 如果源服务器和目标服务器 **未处于相同报表服务器模式下**，例如从本机模式到 SharePoint 模式，并且您使用 SECURITY 开关，则该脚本将尝试基于比较（请参阅主题 [Compare Roles and Tasks in Reporting Services to SharePoint Groups and Permissions](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)）映射默认角色和组。 自定义角色和组不复制到目标服务器。<br /><br /> 在 **处于相同模式下**的服务器之间复制脚本并且使用 SECURITY 开关时，该脚本将在目标服务器上创建新角色（本机模式）或组（SharePoint 模式）。<br /><br /> 如果某一角色已在目标服务器上存在，该脚本将创建如下“失败”消息，并且继续迁移其他项。 在该脚本运行完毕之后，请验证目标服务器上的角色已配置为满足您的需要。 迁移角色:找到8项。<br /><br /> `Migrating role: Browser ... FAILURE: The role 'Browser' already exists and cannot be created. ---> Microsoft.ReportingServices.Diagnostics.Utilities.RoleAlreadyExistsException: The role 'Browser' already exists and cannot be created.`<br /><br /> 有关详细信息，请参阅[授予用户对报表服务器的访问权限（报表管理器）](../security/grant-user-access-to-a-report-server.md)<br /><br /> **注意：** 如果某一用户在源服务器上存在，但在目标服务器上不存在，则该脚本无法在目标服务器上应用角色分配，即使使用了 SECURITY 开关，该脚本也无法应用角色分配。|  
|共享数据源|是|是|该脚本将不覆盖目标服务器上的现有项。 如果目标服务器上已存在同名的项，将显示如下错误消息：<br /><br /> `Migrating DataSource: /Data Sources/Aworks2012_oltp ... FAILURE:The item '/Data Sources/Aworks2012_oltp' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Data Source s/Aworks2012_oltp' already exists.`<br /><br /> 凭据 **不** 作为数据源的一部分被复制。 在迁移内容项后，在目标服务器上更新凭据信息。|  
|共享数据集|是|是||  
|文件夹|是|是|该脚本将不覆盖目标服务器上的现有项。 如果目标服务器上已存在同名的项，将显示如下错误消息：<br /><br /> `Migrating Folder: /Reports ... FAILURE: The item '/Reports' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports' already exists.`|  
|报告|是|是|该脚本将不覆盖目标服务器上的现有项。 如果目标服务器上已存在同名的项，将显示如下错误消息：<br /><br /> `Migrating Report: /Reports/testThe item '/Reports/test' already exists. ---> Microsoft.ReportingServices.Diagnostics.Utilities.ItemAlreadyExistsException: The item '/Reports/test' already exists.`|  
|Parameters|是|是||  
|订阅|是|是||  
|历史记录设置|是|是|将迁移历史记录设置，但不迁移历史记录详细信息。|  
|处理选项|是|是||  
|高速缓存刷新选项|是|是|相关设置作为目录项的一部分迁移。 下面是该脚本的示例，它迁移报表 (.rdl) 以及高速缓存刷新选项之类的相关设置：<br /><br /> 正在迁移报表 TitleOnly.rdl 的参数: 找到了 0 项。<br /><br /> 正在迁移报表 Titleonly.rdl 的订阅:找到1个项目。<br /><br /> 正在迁移作为 \server\public\savedreports 中\\的订阅保存为 titleonly.rdl .。。成功<br /><br /> 正在迁移报表 Titleonly.rdl 的历史记录设置 .。。成功<br /><br /> 正在迁移报表 Titleonly.rdl 的处理选项 .。。找到 0 项。<br /><br /> 正在迁移报表 Titleonly.rdl 的高速缓存刷新选项 .。。成功<br /><br /> 正在迁移报表 Titleonly.rdl 的缓存刷新计划:找到1个项目。<br /><br /> 正在迁移缓存刷新计划 titleonly_refresh735amM2F .。。成功|  
|高速缓存刷新计划|是|是||  
|映像|是|是||  
|报表部件|是|是||  
  
##  <a name="bkmk_required_permissions"></a> 所需的权限  
 读取或写入项和资源的权限并不是对于在该脚本中使用的所有方法全都相同。 下表总结了用于每一项或资源的方法以及相关内容的链接。 导航到单独的主题可看到所需权限。 例如，ListChildren 方法主题记录了以下所需权限：  
  
-   **纯模式所需的权限:** ReadProperties 项  
  
-   **SharePoint 模式所需的权限:** ViewListItems  
  
|项或资源|Source|目标|  
|----------------------|------------|------------|  
|目录项|<xref:ReportService2010.ReportingService2010.ListChildren%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataSourceContents%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemLink%2A>|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.SetItemDataSources%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetItemReferences%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataSource%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateLinkedItem%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateFolder%2A>|  
|Role|<xref:ReportService2010.ReportingService2010.ListRoles%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|  
|系统策略|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|  
|“计划”|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|  
|订阅|<xref:ReportService2010.ReportingService2010.ListSubscriptions%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetSubscriptionProperties%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetDataDrivenSubscriptionProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateSubscription%2A><br /><br /> <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A>|  
|高速缓存刷新计划|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A><br /><br /> <xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|  
|Parameters|<xref:ReportService2010.ReportingService2010.GetItemParameters%2A>|<xref:ReportService2010.ReportingService2010.SetItemParameters%2A>|  
|执行选项|<xref:ReportService2010.ReportingService2010.GetExecutionOptions%2A>|<xref:ReportService2010.ReportingService2010.SetExecutionOptions%2A>|  
|高速缓存选项|<xref:ReportService2010.ReportingService2010.GetCacheOptions%2A>|<xref:ReportService2010.ReportingService2010.SetCacheOptions%2A>|  
|历史记录设置|<xref:ReportService2010.ReportingService2010.GetItemHistoryOptions%2A>|<xref:ReportService2010.ReportingService2010.SetItemHistoryOptions%2A>|  
|项策略|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|  
  
 有关详细信息，请参阅 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)。  
  
##  <a name="bkmk_how_to_use_the_script"></a> 如何使用该脚本  
  
1.  将该脚本文件下载到一个本地文件夹中，例如 **c:\rss\ssrs_migration.rss**。  
  
2.  **使用管理权限**打开命令提示符。  
  
3.  导航到包含 ssrs_migration.rss 文件的文件夹。  
  
4.  使用适合于您的方案的参数运行命令。  
  
 **基本示例，本机模式报表服务器到本机模式报表服务器：**  
  
 下面的示例将本机模式 **Sourceserver** 中的内容迁移到本机模式 **Targetserver**。  
  
 `rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"`  
  
 **使用注意事项：**  
  
-   该脚本分两步运行。  
  
     第一步是审核，以便返回将迁移的项的列表，第二步是迁移过程。  
  
     如果你只想要查看可能的迁移列表或者想要修改参数，则可以在第一步后 **取消该脚本** 。 相关设置不在第一步中列出。 例如，不列出报表的高速缓存选项，而只列出报表本身。  
  
    > [!TIP]  
    >  如果想要仅审核单个服务器，则对源和目标使用相同的服务器并在步骤 1 后取消  
  
     从第一步中获得的审核信息适用于查看源和目标本机模式服务器上的现有角色。 下面是第一步审核列表的示例。 请注意，该列表包含“roles”部分，因为使用了开关-v security="True"：  
  
    -   `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: Model Item Browser`  
  
         `Retrieve and report the list of items that will be migrated. You can cancel the script after step 1 if you do not want to start the actual migration.`  
  
         `Retrieving roles:`  
  
         `Role: Browser`  
  
         `Role: Content Manager`  
  
         `Role: CustomRole`  
  
         `Role: Model Item Browser`  
  
         `Role: My Reports`  
  
         `Role: Publisher`  
  
         `Role: Report Builder`  
  
         `Role: System Administrator`  
  
         `Role: System User`  
  
         `Retrieving system policies:`  
  
         `Retrieving system policies:`  
  
         `System policy: BUILTIN\Administrators`  
  
         `System policy: domain\user1`  
  
         `System policy: domain\ueser2`  
  
         `Retrieving schedules:`  
  
         `Schedule: theMondaySchedule`  
  
         `Retrieving catalog items. This may take a while.`  
  
         `Folder: /Data Sources`  
  
         `DataSource: /Data Sources/Aworks2012_oltp`  
  
         `Folder: /images`  
  
         `Resource: /images/Boba Fett.png`  
  
         `Resource: /images/R2-D2.png`  
  
         `Folder: /Reports`  
  
         `Report: /Reports/products`  
  
         `Report: /Reports/test`  
  
         `Report: /Reports/TitleOnly`  
  
-   SOURCE_URL 和 TARGET_URL 必须是指向源和目标 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表服务器的有效报表服务器 URL。 在本机模式下，报表服务器 URL 如下所示：  
  
    -   `http://servername/reportserver`  
  
     在 SharePoint 模式下，URL 如下所示：  
  
    -   `http://servername/_vti_bin/reportserver`  
  
-   在 SharePoint 中提供给用户的虚拟文件夹结构可能与基础结构不同。 在浏览器中打开 `http://servername/_vti_bin/reportserver` 或 `http://servername/sites/site_name/_vti_bin/reportserver` 可看到非虚拟文件夹结构。 对于 SharePoint 模式下的服务器，这有助于将源文件夹和目标文件夹设置为“/”以外的内容。  
  
-   密码不迁移，并且必须重新输入，例如具有存储的凭据的数据源。  
  
##  <a name="bkmk_parameter_description"></a> 参数说明  
  
|参数|描述|Required|  
|---------------|-----------------|--------------|  
|**-s** Source_URL|源报表服务器的 URL|是|  
|-u Domain\password -p password|源服务器的凭据。|可选，如果缺失则使用默认凭据|  
|**-v st**="SITE"||可选。 此参数仅用于 SharePoint 模式报表服务器。|  
|**- v f**="SOURCEFOLDER"|设置为“/”将迁移所有内容，设置为“/folder/subfolder”之类的项将执行部分迁移。 将复制该文件夹内的所有内容|可选，默认为“/”。|  
|**-v ts**="TARGET_URL"|目标 RS 服务器的 URL||  
|**-v tu**="domain\username" **-v tp**="password"|目标服务器的凭据。|可选，如果缺失则使用默认凭据。 **注意：** 在目标服务器中，用户将作为共享计划的“创建者”以及报表项的“修改者”帐户列出。|  
|**-v tst**="SITE"||可选。 此参数仅用于 SharePoint 模式报表服务器。|  
|**-v tf** ="TARGETFOLDER"|设置为“/”可迁移到根级别中。 设置为“/folder/subfolder”可复制到已存在的目录下。 “SOURCEFOLDER”内的所有内容都将复制到“TARGETFOLDER”。|可选，默认为“/”。|  
|**-v security**= "True/False"|如果设置为“False”，目标目录项将根据目标系统的设置继承安全设置。 这是在不同的报表服务器类型之间进行迁移（例如本机模式到 SharePoint 模式）的推荐设置。 如果设置为“True”，则该脚本将尝试迁移安全设置。|可选，默认值为“False”。|  
  
##  <a name="bkmk_more_examples"></a> 更多示例  
  
###  <a name="bkmk_native_2_native"></a> 本机模式报表服务器到本机模式报表服务器  
 下面的示例将本机模式 **Sourceserver** 中的内容迁移到本机模式 **Targetserver**。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password"  
```  
  
 以下示例添加安全开关：  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p password -v ts="http://TargetServer/reportserver" -v tu="Domain\Userser" -v tp="password" -v security="True"  
```  
  
###  <a name="bkmk_native_2_sharepoint_root"></a> 本机模式到 SharePoint 模式 - 根网站  
 以下示例将内容从本机模式 SourceServer 迁移到 SharePoint 模式服务器 TargetServer 上的“根站点”。 本机模式服务器上的“报表”和“数据源”文件夹作为 SharePoint 部署上的新库迁移。  
  
 ![ssrs_rss_migrate_root_site](../media/ssrs-rss-migrate-root-site.gif "ssrs_rss_migrate_root_site")  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p Password -v ts="http://TargetServer/_vti_bin/ReportServer" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_native_2_sharepoint_with_site"></a> 本机模式到 SharePoint 模式 -“bi”网站集  
 下面的示例将本机模式服务器的内容迁移到包含网站集“sites/bi”和共享文档库的 SharePoint 服务器。 该脚本在目标文档库中创建文件夹。 例如，该脚本在目标文档库中创建“报表”和“数据源”文件夹。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\User -p Password -v ts="http://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_sharepoint_2_sharepoint"></a> SharePoint 模式到 SharePoint 模式 -“bi”网站集  
 下面的示例将迁移内容：  
  
-   从包含网站集“sites/bi”和共享文档库的 SharePoint 服务器 **SourceServer** 。  
  
-   到包含网站集“sites/bi”和共享文档库的 **TargetServer** SharePoint 服务器。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/_vti_bin/reportserver -v st="sites/bi" -v f="Shared Documents" -u Domain\User1 -p Password -v ts="http://TargetServer/sites/bi/_vti_bin/reportserver" -v tst="sites/bi" -v tf="Shared Documents" -v tu="Domain\User" -v tp="Password"  
```  
  
###  <a name="bkmk_native_to_native_Azure_vm"></a>本机模式到本机模式-Azure 虚拟机  
 下面的示例将迁移内容：  
  
-   从本机模式报表服务器 **SourceServer**。  
  
-   Report Server 在 Azure 虚拟机上运行的**TargetServer**本机模式。 TargetServer 未加入**SourceServer**的域, 并且是 Azure 虚拟机 **TargetServer**上的管理员。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://SourceServer/ReportServer -u Domain\user1 -p Password -v ts="http://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Password2"  
```  
  
> [!TIP]  
>  有关如何使用 Windows powershell 在 Azure 虚拟机上[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]创建报表服务器的信息, 请参阅[使用 PowerShell 创建具有本机模式报表服务器的 azure VM](https://msdn.microsoft.com/library/dn449661.aspx)。  
  
##  <a name="bkmk_sharepoint_site_to_native_Azure_vm"></a>SharePoint 模式-Azure 虚拟机上的本机模式服务器的 "bi" 网站集  
 下面的示例将迁移内容：  
  
-   从包含网站集 “sites/bi” 和共享文档库的 SharePoint 模式报表服务器 **SourceServer** 。  
  
-   Report Server 在 Azure 虚拟机上运行的**TargetServer**本机模式。 TargetServer 未加入**SourceServer**的域, 并且是 Azure 虚拟机 **TargetServer**上的管理员。  
  
```  
rs.exe -i ssrs_migration.rss -e Mgmt2010 -s http://uetesta02/_vti_bin/reportserver -u user1 -p Password -v ts="http://ssrsnativeazure.cloudapp.net/ReportServer" -v tu="user2" -v tp="Passowrd2"  
```  
  
##  <a name="bkmk_verification"></a> 验证  
 本节总结了为验证内容和策略是否已成功迁移而在目标服务器上要执行的一些步骤。  
  
### <a name="schedules"></a>“计划”  
 验证目标服务器上的计划：  
  
 **Native Mode**  
  
1.  浏览到目标服务器上的报表管理器。  
  
2.  在顶部菜单上，单击 **“网站设置”** 。  
  
3.  在左窗格中，单击 **“计划”** 。  
  
 **SharePoint 模式：**  
  
1.  浏览至“站点设置”。  
  
2.  在 **Reporting Services** 组中，单击 **“管理共享计划”** 。  
  
### <a name="roles-and-groups"></a>角色和组  
 **Native Mode**  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 并且连接到您的本机模式报表服务器。  
  
2.  在 **“对象资源管理器”** 中，单击 **“安全性”** 。  
  
3.  单击 **“角色”** 。  
  
##  <a name="bkmk_troubleshoot"></a> 故障排除  
 使用跟踪标志“-t”可获得详细信息。 例如，如果您运行此脚本并看到如下消息  
  
-   无法连接到服务器： http://\<servername>/ReportServer/ReportService2010.asmx  
  
 使用 **-t**标志再次运行该脚本, 以查看类似于以下内容的消息:  
  
-   System.exception:无法连接到服务器: http://\<servername >/ReportServer/ReportService2010.asmx---> 系统 WebException:**请求失败, HTTP 状态为 401:未经**授权。   在 System.Web.Services.Protocols.SoapHttpClientProtocol.ReadResponse （SoapClientMessage 消息、 WebResponse 响应、 流 responseStream、 布尔值 asyncCall） 在 System.Web.Services.Protocols.SoapHttpClientProtocol.Invoke （字符串方法名称，对象 [] 参数） 在 Microsoft.SqlServer.ReportingServices2010.ReportingService2010.IsSSLRequired() 在 Microsoft.ReportingServices.ScriptHost.Management2010Endpoint.PingService （字符串 url、 String userName、 字符串密码字符串域、 Int32 超时) 在 Microsoft.ReportingServices.ScriptHost.ScriptHost.DetermineServerUrlSecurity()-内部异常堆栈跟踪结束----  
  
## <a name="see-also"></a>请参阅  
 [RS.exe 实用工具 (SSRS)](rs-exe-utility-ssrs.md)   
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
  
