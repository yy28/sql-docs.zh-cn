---
title: "部署数据层应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-tier-apps"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.deploydacwizard.introduction.f1"
  - "sql13.swb.deploydacwizard.deploydac.f1"
  - "sql13.swb.deploydacwizard.summary.f1"
  - "sql13.swb.deploydacwizard.updateconfiguration.f1"
  - "sql13.swb.deploydacwizard.selectdac.f1"
helpviewer_keywords: 
  - "部署数据层应用程序"
  - "部署 DAC"
  - "数据层应用程序 [SQL Server], 部署"
  - "操作指南 [DAC], 部署"
  - "向导 [DAC], 部署"
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
caps.latest.revision: 33
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 32
---
# 部署数据层应用程序
  您可使用向导或 PowerShell 脚本将数据层应用程序 (DAC) 从 DAC 包部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的现有实例。 该部署过程通过在 **msdb** 系统数据库（在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中为 **master**）中存储 DAC 定义来注册一个 DAC 实例，创建一个数据库，然后使用在该 DAC 中定义的所有数据库对象来填充该数据库。  
  
-   **开始之前：**  [SQL Server 实用工具](#SQLUtility)、 [数据库选项和设置](#DBOptSettings)、 [限制和局限](#LimitationsRestrictions)、 [先决条件](#Prerequisites)、 [安全性](#Security)、 [权限](#Permissions)  
  
-   **若要部署 DAC，请使用：**[部署数据层应用程序向导](#UsingDeployDACWizard)、[PowerShell](#DeployDACPowerShell)  
  
##  <a name="BeforeBegin"></a> 开始之前  
 同一 DAC 包可以多次部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的单个实例上，但必须一次一个执行这些部署。 为每个部署指定的 DAC 实例名称在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中必须唯一。  
  
###  <a name="SQLUtility"></a> SQL Server 实用工具  
 如果您将 DAC 部署到数据库引擎的托管实例，在下次将实用工具收集组从该实例发送到实用工具控制点时，部署的 DAC 将合并到 SQL Server 实用工具中。 然后，该 DAC 将出现在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]“实用工具资源管理器”的“已部署的数据层应用程序”节点下，并且在“已部署的数据层应用程序”详细信息页中报告。  
  
###  <a name="DBOptSettings"></a> 数据库选项和设置  
 默认情况下，在部署过程中创建的数据库将具有来自 CREATE DATABASE 语句的几乎所有默认设置，只有以下方面除外：  
  
-   数据库排序规则和兼容级别设置为在 DAC 包中定义的值。 从 SQL Server 开发工具的数据库项目生成的 DAC 包使用在数据库项目中设置的值。 从现有数据库中提取的包将使用来自原始数据库的值。  
  
-   您可以在 **“更新配置”** 页中调整某些数据库设置，例如数据库名称和文件路径。 在部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 时，不能设置文件路径。  
  
 某些数据库选项（例如 TRUSTWORTHY、DB_CHAINING 和 HONOR_BROKER_PRIORITY）不能作为部署过程的一部分进行调整。 物理属性（例如文件组的数目或者文件的数目和大小）不能作为部署过程的一部分进行更改。 在部署完成后，可以使用 ALTER DATABASE 语句、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 对数据库进行定制。  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
 可以将 DAC 部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 或运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 4 (SP4) 或更高版本的[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例。 如果使用更高版本创建 DAC，则 DAC 可能包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 不支持的对象。 您不能将这些 DAC 部署到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]实例。  
  
###  <a name="Prerequisites"></a> 先决条件  
 建议您不要从未知或不可信源部署 DAC 包。 此类包可能包含恶意代码，这些代码可能会执行非预期的 Transact-SQL 代码，或者通过修改架构导致错误。 在使用来自未知或不可信源的包之前，请解压缩该 DAC 并检查代码，例如存储过程或者其他用户定义的代码。 有关如何执行这些检查的详细信息，请参阅 [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md)。  
  
###  <a name="Security"></a> 安全性  
 为了提高安全性，SQL Server 身份验证登录名存储在 DAC 包中且没有密码。 在部署或升级该包时，登录名将作为含有生成的密码的已禁用登录名创建。 若要启用这些登录名，请使用具有 ALTER ANY LOGIN 权限的登录名登录，并且使用 ALTER LOGIN 来启用该登录名并且分配可以传达给用户的新密码。 对于 Windows 身份验证登录名则无需执行此操作，因为其密码不是由 SQL Server 管理的。  
  
####  <a name="Permissions"></a> 权限  
 DAC 只能由 **sysadmin** 或 **serveradmin** 固定服务器角色的成员部署，或者由属于 **dbcreator** 固定服务器角色并具有 ALTER ANY LOGIN 权限的登录名部署。 名为 **sa** 的内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员帐户也可以部署 DAC。 将具有登录名的 DAC 部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 要求 loginmanager 或 serveradmin 角色的成员身份。 将不带登录名的 DAC 部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 要求 dbmanager 或 serveradmin 角色的成员身份。  
  
##  <a name="UsingDeployDACWizard"></a> 使用“部署数据层应用程序向导”  
 **使用向导部署 DAC**  
  
1.  在 **“对象资源管理器”**中，展开要将 DAC 部署到的实例的节点。  
  
2.  右键单击“数据库”节点，然后选择“部署数据层应用程序…”  
  
3.  完成向导对话框：  
  
    -   [“简介”页](#Introduction)  
  
    -   [“选择 DAC 包”页](#Select_dac_package)  
  
    -   [“查看策略”页](#Review_policy)  
  
    -   [“更新配置”页](#Update_configuration)  
  
    -   [摘要页](#Summary)  
  
    -   [“部署”页](#Deploy)  
  
##  <a name="Introduction"></a> “简介”页  
 此页描述数据层应用程序的部署步骤。  
  
 **不再显示此页。** - 选中该复选框可以停止在将来显示此页。  
  
 “下一步 >” - 继续到“选择 DAC 包”页。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="Select_dac_package"></a> “选择 DAC 包”页  
 使用此页可以指定包含要部署的数据层应用程序的 DAC 包。 该页可为三种状态。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
### 选择 DAC 包  
 使用该页的初始状态可以选择要部署的 DAC 包。 该 DAC 包必须是有效的 DAC 包文件，并且必须具有 .dacpac 扩展名。  
  
 “DAC 包”- 指定包含要部署的数据层应用程序的 DAC 包的路径和文件名。 您可以选择框右侧的 **“浏览”** 按钮以便浏览到 DAC 包的位置。  
  
 “应用程序名称” - 一个只读框，它显示创作 DAC 或者从某一数据库中提取 DAC 时分配的 DAC 名称。  
  
 “版本”- 一个只读框，它显示创作 DAC 或者从某一数据库中提取 DAC 时分配的版本。  
  
 “说明”- 一个只读框，它显示创作 DAC 或者从某一数据库中提取 DAC 时编写的版本。  
  
 **\< 上一步** - 返回到“简介”页。  
  
 “下一步 >”- 显示进度栏，因为向导已确认所选文件为有效的 DAC 包。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
### 验证 DAC 包  
 在向导确认所选文件是有效的 DAC 包时显示一个进度栏。 如果对该 DAC 包进行了验证，则向导将继续到 **“选择包”** 页的最终形式，从中可以查看验证的结果。 如果该文件不是有效的 DAC 包，则向导会保持在 **“选择 DAC 包”**页上。 或者选择另一个有效的 DAC 包，或者取消该向导并且生成一个新的 DAC 包。  
  
 “正在验证 DAC 的内容”- 报告验证过程的当前状态的进度栏。  
  
 “\< 上一步”- 返回到“选择包”页的初始状态。  
  
 “下一步 >”- 继续到“选择包”页的最终版本。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="Review_policy"></a> “查看策略”页  
 使用此页可查看评估 DAC 服务器选择策略的结果（如果该 DAC 具有策略）。 该 DAC 服务器选择策略是可选的，并在 Visual Studio 中创建它时分配给该 DAC。 该策略使用该服务器选择策略方面指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例为承载该 DAC 而必须满足的条件。  
  
 “策略条件的评估结果”- 一个只读报告，显示 DAC 部署策略的条件是否成功。 将在单独的行上报告对每个条件进行评估的结果。  
  
 在将 DAC 部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 时以下服务器选择策略的计算结果始终为 false：操作系统版本、语言、启用的命名管道、平台和启用的 tcp。  
  
 “忽略违反策略情况”- 使用此复选框可以在未能满足一个或多个策略条件的情况下继续进行部署。 只有在您确保未满足的所有条件都不会阻碍 DAC 操作成功条件的情况下，才选择此选项。  
  
 “\< 上一步”- 返回到“选择包”页。  
  
 “下一步 >”- 继续到“更新配置”页。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="Update_configuration"></a> “更新配置”页  
 使用此页可指定已部署的 DAC 实例的名称以及部署创建的数据库的名称，并且可设置数据库选项。  
  
 “数据库名称”：- 指定要由部署创建的数据库的名称。 默认值是从其提取该 DAC 的源数据库的名称。 该名称在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例内必须唯一，并且必须符合 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 标识符的规则。  
  
 如果您更改数据库名称，则数据文件和日志文件的名称也将更改以匹配这个新值。  
  
 该数据库名称还用作 DAC 实例的名称。 该实例名称显示在“对象资源管理器”中“数据层应用程序”节点下的 DAC 的节点上，或者显示在“实用工具资源管理器”中“已部署的数据层应用程序”节点下的 DAC 的节点上。  
  
 以下选项不应用于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，并且在部署到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 时不显示。  
  
 “使用默认数据库位置”- 选择此选项可在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的默认位置中创建数据库数据和日志文件。 将使用数据库名称生成文件名。  
  
 “指定数据库文件”- 选择此选项可为数据文件和日志文件指定其他位置或名称。  
  
 “数据文件路径和名称”：- 指定数据文件的完整路径和文件名。 该框将用默认路径和文件名填充。 编辑该框中的字符串可以更改默认值，或者使用“浏览”按钮可以导航到要用于放置数据文件的文件夹。  
  
 “日志文件路径和名称”：- 指定日志文件的完整路径和文件名。 该框将用默认路径和文件名填充。 编辑该框中的字符串可以更改默认值，或者使用 **“浏览”** 按钮可以导航到要用于放置日志文件的文件夹。  
  
 “\< 上一步”- 返回到“选择 DAC 包”页。  
  
 “下一步 >”- 继续到“摘要”页。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="Summary"></a> 摘要页  
 使用此页可以查看在部署 DAC 时向导将执行的操作。  
  
 **将使用以下设置部署 DAC。** - 查看显示的信息以便确保将执行的操作正确。 该窗口显示您选择的 DAC 包，以及您为部署的 DAC 实例选择的名称。 该窗口还显示在创建与该 DAC 相关联的数据库时将使用的设置。  
  
 “\< 上一步”- 返回到“更新配置”页以更改你的选择。  
  
 “下一步 >”- 部署 DAC，并在“部署 DAC”页中显示结果。  
  
 “取消”- 终止向导且不部署 DAC。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="Deploy"></a> “部署”页  
 此页报告部署操作是成功还是失败。  
  
 “部署 DAC”- 报告为部署 DAC 而执行的每个操作是成功还是失败。 查看信息以便确定每个操作是成功还是失败。 遇到了错误的任何操作都将在 **“结果”** 列中具有一个链接。 选择该链接可以查看针对该操作的错误报告。  
  
 “保存报表”- 选择此按钮可以将部署报表保存到某一 HTML 文件。 该文件报告每个操作的状态，并且包括任何操作生成的所有错误。 默认文件夹是您的 Windows 帐户的 Documents 文件夹中的 SQL Server Management Studio\DAC Packages 文件夹。  
  
 “完成”- 终止向导。  
  
 [[部署向导]](#UsingDeployDACWizard)  
  
##  <a name="DeployDACPowerShell"></a> 使用 PowerShell  
 **在 PowerShell 脚本中使用 Install() 方法部署 DAC**  
  
1.  创建一个 SMO Server 对象，并将该对象设置为要将 DAC 部署到的实例。  
  
2.  打开 **ServerConnection** 对象，并连接到同一实例。  
  
3.  使用 **System.IO.File** 加载 DAC 包文件。  
  
4.  使用 **add_DacActionStarted** 和 **add_DacActionFinished** 订阅 DAC 部署事件。  
  
5.  设置 **DatabaseDeploymentProperties**。  
  
6.  使用 **DacStore.Install** 方法部署 DAC。  
  
7.  关闭用于读取 DAC 包文件的文件流。  
  
### 示例 (PowerShell)  
 下面的示例使用来自 MyApplication.dacpac 包的 DAC 定义，将名为 MyApplication 的 DAC 部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]的默认实例。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## 另请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [从数据库中提取 DAC](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [数据库标识符](../../relational-databases/databases/database-identifiers.md)  
  
  