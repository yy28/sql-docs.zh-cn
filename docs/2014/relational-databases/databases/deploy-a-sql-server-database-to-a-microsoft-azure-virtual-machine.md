---
title: 将 SQL Server 数据库部署到 Microsoft Azure 虚拟机 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7d84fbe56d36bd91f2b7f8b49a3df73fb383c6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "70175736"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>将 SQL Server 数据库部署到 Microsoft Azure 虚拟机
  使用 "将**SQL Server 数据库部署到 AZURE VM** " 向导，将数据库从的[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例部署到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] azure 虚拟机（VM）中的。 此向导利用完整数据库备份操作，因此可始终复制 SQL Server 用户数据库中的完整数据架构和数据。 此向导还为您进行所有 Azure VM 配置，因此不需要预先配置 VM。  
  
 您无法使用此向导进行差异备份，因为此向导将不会覆盖具有相同的数据库名称的现有数据库。 若要替换 VM 上的现有数据库，必须先删除现有数据库或更改数据库名称。 如果在未提交的部署操作的数据库名称与 VM 上的现有数据库之间存在命名冲突，此向导将建议为未提交的数据库追加数据库名称以便您能完成操作。  
  
##  <a name="before_you_begin"></a> 开始之前  
 若要完成此向导，您必须能够提供以下信息并准备好以下这些配置设置：  
  
-   与 Azure 订阅关联的 Microsoft 帐户详细信息。  
  
-   你的 Azure 发布配置文件。  
  
    > [!CAUTION]  
    >  SQL Server 当前支持发布配置文件版本 2.0。 要下载支持的发布配置文件版本，请参阅 [下载发布配置文件 2.0](https://go.microsoft.com/fwlink/?LinkId=396421)。  
  
-   已上传到 Azure 订阅的管理证书。  
  
-   保存到运行向导的计算机上个人证书存储区中的管理证书。  
  
-   您必须具有可供承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的计算机使用的临时存储位置。 该临时存储位置还必须可供运行向导的计算机使用。  
  
-   如果将数据库部署到现有虚拟机，则必须将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置为侦听 TCP/IP 端口。  
  
-   你计划用于创建 VM 的 Azure VM 或库映像必须配置并运行 SQL Server 云适配器。  
  
-   必须使用专用端口11435在 Azure 网关上配置 SQL Server 云适配器的开放终结点。  
  
 此外，如果您计划将数据库部署到现有的 Azure VM，则还必须能够提供：  
  
-   承载该虚拟机的云服务的 DNS 名称。  
  
-   虚拟机的管理员凭据。  
  
-   对要部署的数据库具有备份操作员权限的凭据，它们来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的源实例。  
  
 有关在 Azure 虚拟机中运行 SQL Server 的详细信息，请参阅[准备迁移到 Azure 虚拟机中的 SQL Server](https://msdn.microsoft.com/library/dn133142.aspx)。  
  
 在运行 Windows Server 操作系统的计算机上，您必须使用以下配置设置来运行此向导：  
  
-   禁用增强安全性配置：使用“服务器管理器”>“本地服务器”将 Internet Explorer 增强安全性配置 (ESC) 设置为“OFF”****。  
  
-   启用 JavaScript：“Internet Explorer”>“Internet 选项”>“安全性”>“客户级别”>“脚本”>“活动脚本”：“启用”****。  
  
###  <a name="limitations"></a> 限制和局限  
 针对此操作的数据库大小限制为 1 TB。  
  
 适用于 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]的 SQL Server Management Studio 中提供了此部署功能。  
  
 此部署功能仅适用于用户数据库；不支持部署系统数据库。  
  
 此部署功能不支持与地缘组相关联的托管服务。 例如，在此向导的 **“部署设置”** 页上无法选择与某一地缘组相关联的存储帐户以供使用。  
  
 虚拟机中的 SQL Server 版本必须等于或高于源 SQL Server 版本。 可以使用此向导 SQL Server 可以部署到 Azure VM 的数据库版本：  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 在 Azure VM 数据库中运行 SQL Server 数据库版本可部署到：  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 如果在未提交的部署操作的数据库名称与 VM 上的现有数据库之间存在命名冲突，此向导将建议为未提交的数据库追加数据库名称以便您能完成操作。  
  
###  <a name="filestream"></a>将启用了 FILESTREAM 的数据库部署到 Azure VM 时的注意事项  
 在部署其 BLOBS 存储于 FILESTREAM 对象中的数据库时，请注意以下准则和限制：  
  
-   部署功能不能将支持 FILESTREAM 的数据库部署到一个新的 VM 中。 如果在运行该向导前没有在 VM 中启用 FILESTREAM，则数据库还原操作将失败，并且向导操作将不能成功完成。 若要成功部署使用 FILESTREAM 的数据库，请在启动该向导前在宿主 VM 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中启用 FILESTREAM。 有关详细信息，请参阅 [FILESTREAM (SQL Server)](https://msdn.microsoft.com/library/gg471497.aspx)。  
  
-   如果您的数据库使用内存中 OLTP，则无需对该数据库进行任何修改即可将它部署到 Azure VM 中。 有关详细信息，请参阅 [内存中 OLTP（内存中优化）](https://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx)。  
  
###  <a name="geography"></a>针对资产的地理分布的注意事项  
 请注意，以下资产必须位于相同地理区域中：  
  
-   云服务  
  
-   VM 位置  
  
-   数据磁盘存储服务  
  
 如果上面列出的资产未共置在一起，则该向导将无法成功完成。  
  
###  <a name="configuration_settings"></a>向导配置设置  
 使用以下配置详细信息可修改针对部署到 Azure VM 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库部署设置。  
  
-   **配置文件的默认路径**-%LOCALAPPDATA%\SQL SERVER\DEPLOY TO to SQL in WA VM\DeploymentSettings.xml  
  
-   **配置文件结构**  
  
    -   \<Deploymentsettings.json>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- 日志记录级别 -->  
  
            -   BackupPath="\\\\[server name]\\[volume]\\" \<!-- 最后使用的备份路径。 Used as default in the wizard. -->  
  
            -   CleanupDisabled = False/> \<!--向导将不会删除中间文件和 Azure 对象（VM、CS、SA）。 -->  
  
        -   <PublishProfile \<!-- 最后使用的发布配置文件信息。 -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- 在向导中使用的证书。 -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- 在向导中使用的订阅。 -->  
  
            -   Name="My Subscription" \<!-- 订阅名称。 -->  
  
            -   Publisher="" />  
  
    -   
  \</DeploymentSettings>  
  
 **配置文件值**  
  
###  <a name="permissions"></a> 权限  
 所部署的数据库必须处于正常状态，该数据库必须可供运行向导的用户帐户访问，而且该用户帐户必须拥有执行备份操作的权限。  
  
##  <a name="launch_wizard"></a>使用 "将数据库部署到 Azure VM" 向导  
 **若要启动向导，则使用以下步骤：**  
  
1.  使用 SQL Server Management Studio 连接到具有要部署的数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
2.  在 **对象资源管理器**中，展开该实例名称，然后展开 **“数据库”** 节点。  
  
3.  右键单击要部署的数据库，选择 "**任务**"，然后选择 "**将数据库部署到 Azure VM ...** "  
  

  
##  <a name="Introduction"></a> “简介”页  
 本页介绍如何将**SQL Server 数据库部署到 AZURE VM**向导。  
  
 **选项**  
  
-   **不再显示此页。** - 单击此复选框可以阻止在将来显示“简介”页。  
  
-   **下一步**-继续到 "**源设置**" 页。  
  
-   **取消** - 取消操作并关闭向导。  
  
-   **Help** -启动向导的 MSDN 帮助主题。  
  
##  <a name="Source_settings"></a>源设置  
 使用此页可连接到承载要部署[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 Azure VM 的数据库的实例。 还将指定一个临时位置，以便在将文件传输到 Azure 之前从本地计算机保存文件。 这可以是共享网络位置。  
  
 **选项**  
  
-   单击 "**连接 ...** "，然后为承载要部署的数据库的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例指定连接详细信息。  
  
-   使用 **“选择数据库”** 下拉列表来指定要部署的数据库。  
  
-   在 "**其他设置**" 字段中，指定可供 Azure VM 服务访问的共享文件夹。  
  
##  <a name="Azure_sign-in"></a>Azure 登录  
 使用此页连接到 Azure 并提供管理证书或发布配置文件详细信息。  
  
 **选项**  
  
-   **管理证书**-使用此选项来指定本地证书存储区中与 Azure 中的管理证书匹配的证书。  
  
-   **发布配置文件**-如果已将发布配置文件下载到计算机，请使用此选项。  
  
-   **登录**-使用此选项可以使用 Microsoft 帐户（例如，Live ID 或 Hotmail 帐户）登录到 Azure，以生成并下载新管理证书。 请注意，每个订阅的证书数目是有限的。  
  
-   **订阅**-选择、键入或粘贴与本地证书存储中的管理证书或发布配置文件相匹配的 AZURE 订阅 ID。  
  
##  <a name="Deployment_settings"></a>部署设置页  
 使用此页可以指定目标服务器并提供有关新数据库的详细信息。  
  
 **选项**  
  
-   **Azure 虚拟机**-指定将承载 SQL Server 数据库的 VM 的详细信息：  
  
-   **云服务名称**-指定承载虚拟机的服务的名称。 要创建新的云服务，请指定该服务的名称。  
  
-   **虚拟机名称**-指定将承载 SQL Server 数据库的 VM 的名称。 若要创建新的 Azure VM，请指定新 VM 的名称。  
  
-   **设置**-使用 "设置" 按钮创建一个新的 VM 以托管 SQL Server 数据库。 如果使用的是现有虚拟机，您提供的信息将用于对您的凭据进行身份验证。  
  
-   **存储帐户**-从下拉列表中选择存储帐户。 要创建新的存储帐户，请指定该帐户的名称。 请注意，在下拉列表中将不会提供与某一地缘组相关联的存储帐户。  
  
-   **目标数据库**-指定目标数据库的详细信息。  
  
-   **服务器连接**-服务器的连接详细信息。  
  
-   **数据库**-指定或确认新数据库的名称。 如果数据库名称在目标 SQL Server 实例上已存在，建议您修改该名称。  
  
##  <a name="Summary"></a> 摘要页  
 使用此页可查看操作的指定设置。 若要使用指定设置完成部署操作，请单击 **“完成”**。 若要取消部署操作并退出向导，请单击 **“取消”**。  
  
 将数据库详细信息部署到 Azure VM 上的 SQL Server 数据库可能需要手动步骤。 将为您详细说明这些步骤。  
  
##  <a name="Results"></a> “结果”页  
 此页将报告部署操作是成功还是失败，并显示每个操作的结果。 遇到了错误的任何操作都将在 **“结果”** 列中具有一个指示。 单击该链接可以查看针对该操作的错误报告。  
  
 单击 **“完成”** 关闭向导。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 的云适配器](../../database-engine/cloud-adapter-for-sql-server.md)   
 [数据库生命周期管理](../database-lifecycle-management.md)   
 [导出数据层应用程序](../data-tier-applications/export-a-data-tier-application.md)   
 [导入 BACPAC 文件以创建新的用户数据库](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Azure SQL 数据库备份和还原](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [在 Azure 虚拟机中部署 SQL Server](https://msdn.microsoft.com/library/dn133141.aspx)   
 [准备迁移到 Azure 虚拟机中的 SQL Server](https://msdn.microsoft.com/library/dn133142.aspx)  
  
  
