---
title: 使用 DAC 部署数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dbdeployment.settings.f1
- sql12.swb.dbdeployment.progress.f1
- sql12.swb.dbdeployment.summary.f1
- sql12.swb.dbdeployment.results.f1
- sql12.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 03233cc3a35818352c3a8875f62610b5a0814522
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050469"
---
# <a name="deploy-a-database-by-using-a-dac"></a>使用 DAC 部署数据库
  使用“将数据库部署到 SQL Azure”  向导在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例与 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器之间，或在两台 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]服务器之间部署数据库。  
  
##  <a name="BeforeBegin"></a> 开始之前  
 该向导使用数据层应用程序 (DAC) BACPAC 存档文件部署数据库对象的数据和定义。 它从源数据库执行 DAC 导出操作，并对目标执行 DAC 导入。  
  
###  <a name="DBOptSettings"></a> 数据库选项和设置  
 默认情况下，在部署过程中创建的数据库将具有来自 CREATE DATABASE 语句的默认设置。 例外是数据库集合和兼容级别将设置为源数据库中的值。  
  
 数据库选项（如 TRUSTWORTHY、DB_CHAINING 和 HONOR_BROKER_PRIORITY）不能作为部署过程的一部分进行调整。 物理属性（例如文件组的数目或者文件的数目和大小）不能作为部署过程的一部分进行更改。 在部署完成后，可以使用 ALTER DATABASE 语句、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 对数据库进行定制。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 **“部署数据库”** 向导支持：  
  
-   将数据库从 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例部署到 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
-   将数据库从 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
-   在两台 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器之间部署数据库。  
  
 此向导不支持在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的两个实例之间部署数据库。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例必须运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更高版本才能使用此向导。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例上的数据库包含 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]上不支持的对象，则无法使用该向导将数据库部署到 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 如果 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 上的数据库包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持的对象，则您无法使用该向导将数据库部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
###  <a name="Security"></a> 安全性  
 为了提高安全性，SQL Server 身份验证登录名存储在 DAC BACPAC 文件中且没有密码。 在导入此 BACPAC 时，登录名将作为含有生成的密码的已禁用登录名创建。 若要启用这些登录名，请使用具有 ALTER ANY LOGIN 权限的登录名登录，并且使用 ALTER LOGIN 来启用该登录名并且分配可以传达给用户的新密码。 对于 Windows 身份验证登录名则无需执行此操作，因为其密码不是由 SQL Server 管理的。  
  
#### <a name="permissions"></a>Permissions  
 此向导需要对源数据库具有 DAC 导出权限。 登录名至少要求 ALTER ANY LOGIN 和数据库作用域 VIEW DEFINITION 权限，以及对 **sys.sql_expression_dependencies**具有 SELECT 权限。 导出 DAC 可由 securityadmin 固定服务器角色的成员（也是从其导出 DAC 的数据库中 database_owner 固定数据库角色的成员）完成。 sysadmin 固定服务器角色的成员或名为 **sa** 的内置 SQL Server 系统管理员帐户也可以导出 DAC。  
  
 此向导需要对目标实例或服务器的 DAC 导入权限。 登录名必须是 **sysadmin** 或 **serveradmin** 固定服务器角色的成员，或者是 **dbcreator** 固定服务器角色的成员并且具有 ALTER ANY LOGIN 权限。 名为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **的内置** 系统管理员帐户也可以导入 DAC。 将具有登录名的 DAC 导入到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 要求 loginmanager 或 serveradmin 角色的成员身份。 将不具有登录名的 DAC 导入到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 要求 dbmanager 或 serveradmin 角色的成员身份。  
  
##  <a name="UsingDeployDACWizard"></a> 使用部署数据库向导  
 **使用部署数据库向导迁移数据库**  
  
1.  连接到您要部署的数据库的位置。 只能指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器。  
  
2.  在 **“对象资源管理器”** 中，展开包含数据库的实例的节点。  
  
3.  展开 **“数据库”** 节点。  
  
4.  右键单击要部署的数据库，选择 **“任务”**，然后选择 **“将数据库部署到 SQL Azure…”**  
  
5.  完成向导对话框：  
  
    -   [“简介”页](#Introduction)  
  
    -   [部署设置](#Deployment_settings)  
  
    -   [摘要页](#Summary)  
  
    -   [结果](#Results)  
  
##  <a name="Introduction"></a> “简介”页  
 此页说明 **“部署数据库”** 向导的步骤。  
  
 **选项**  
  
-   **不再显示此页。** - 选中此复选框可以停止在将来显示“简介”页。  
  
-   **下一步** - 进入 **“部署设置”** 页。  
  
-   **取消** – 取消操作并关闭向导。  
  
##  <a name="Deployment_settings"></a> “部署设置”页  
 使用此页可以指定目标服务器并提供有关新数据库的详细信息。  
  
 **本地主机：**  
  
-   **服务器连接** – 指定服务器连接详细信息，然后单击 **“连接”** 来验证连接。  
  
-   **新数据名称** – 指定新数据库的名称。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据库设置：**  
  
-   **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 版本** – 从下拉菜单中选择 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的版本。  
  
-   **最大数据库大小** – 从下拉菜单中选择最大数据库大小。  
  
 **其他设置：**  
  
-   指定临时文件的本地目录，该文件为 BACPAC 存档文件。 请注意，将在指定位置创建此文件，并且在操作完成后，此文件将保留在该位置。  
  
##  <a name="Summary"></a> 摘要页  
 使用此页可查看操作的指定的源和目标设置。 若要使用指定设置完成部署操作，请单击 **“完成”**。 若要取消部署操作并退出向导，请单击 **“取消”**。  
  
##  <a name="Progress"></a> “进度”页  
 此页将显示一个指示操作状态的进度栏。 若要查看详细状态，请单击 **“查看详细信息”** 选项。  
  
##  <a name="Results"></a> “结果”页  
 此页将报告部署操作是成功还是失败，并显示每个操作的结果。 遇到了错误的任何操作都将在 **“结果”** 列中具有一个链接。 单击该链接可以查看针对该操作的错误报告。  
  
 单击 **“完成”** 关闭向导。  
  
## <a name="using-a-net-framework-application"></a>使用 .Net Framework 应用程序  
 **使用 .Net Framework 应用程序中的 DacStoreExport() 和 Import() 方法来部署数据库。**  
  
 若要查看代码示例，请下载有关 [Codeplex](http://go.microsoft.com/fwlink/?LinkId=219575)的 DAC 示例应用程序  
  
1.  创建一个 SMO Server 对象，并将该对象设置为包含要部署的数据库的实例或服务器。  
  
2.  打开`ServerConnection`对象，并连接到同一实例。  
  
3.  使用`Export`方法的`Microsoft.SqlServer.Management.Dac.DacStore`类型将数据库导出到 BACPAC 文件。 指定要导出的数据库的名称以及指向将用于放置 BACPAC 文件的文件夹的路径。  
  
4.  创建一个 SMO Server 对象，并将该对象设置为目标实例或服务器。  
  
5.  打开`ServerConnection`对象，并连接到同一实例。  
  
6.  使用`Import`方法的`Microsoft.SqlServer.Management.Dac.DacStore`类型导入 BACPAC。 指定导出创建的 BACPAC 文件。  
  
## <a name="see-also"></a>请参阅  
 [数据层应用程序](data-tier-applications.md)   
 [导出数据层应用程序](export-a-data-tier-application.md)   
 [导入 BACPAC 文件以创建新的用户数据库](import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
