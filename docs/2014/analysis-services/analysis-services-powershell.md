---
title: Analysis Services PowerShell |Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f75298a4701f15a1fc0f3f471bf7628f4a7030c1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782644"
---
# <a name="analysis-services-powershell"></a>Analysis Services PowerShell
  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 包括 Analysis Services PowerShell (SQLAS) 提供程序和 cmdlet，以便您可以使用 Windows PowerShell 导航、管理和查询 Analysis Services 对象。  
  
 Analysis Services PowerShell 由以下组件构成：  
  
-   用于导航分析管理对象 (AMO) 层次结构的 `SQLAS` 提供程序。  
  
-   用于执行 MDX、DMX 或 XMLA 脚本的 `Invoke-ASCmd` cmdlet。  
  
-   用于日常操作（例如处理、角色管理、分区管理、备份和还原）的特定于任务的 cmdlet。  
  
## <a name="in-this-article"></a>本文内容  
 [先决条件](#bkmk_prereq)  
  
 [Analysis Services 支持的版本和模式](#bkmk_vers)  
  
 [身份验证要求和安全注意事项](#bkmk_auth)  
  
 [Analysis Services PowerShell 任务](#bkmk_tasks)  

有关语法和示例的详细信息，请参阅[Analysis Services PowerShell 参考](/sql/analysis-services/powershell/analysis-services-powershell-reference)。

##  <a name="prerequisites"></a><a name="bkmk_prereq"></a>先决条件  
 必须安装有 Windows PowerShell 2.0。 该软件默认安装在 Windows 操作系统的较新版本上。 有关详细信息，请参阅[安装 Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 您必须安装包括 SQL Server PowerShell (SQLPS) 模块和客户端库在内的 SQL Server 功能。 最简单的操作方式是安装 SQL Server Management Studio，其中自动包括 PowerShell 功能和客户端库。 SQL Server PowerShell (SQLPS) 模块包含用于所有 SQL Server 功能的 PowerShell 提供程序和 cmdlet，包括用于导航 Analysis Services 对象层次结构的 SQLASCmdlets 模块和 SQLAS 提供程序。  
  
 你必须导入**SQLPS**模块，然后才能使用该`SQLAS`提供程序和 cmdlet。 SQLAS 提供程序是`SQLServer`提供程序的扩展。 有几种方法可以导入 SQLPS 模块。 有关详细信息，请参阅 [导入 SQLPS 模块](../../2014/database-engine/import-the-sqlps-module.md)。  
  
 远程访问 Analysis Services 实例要求您启用远程管理和文件共享。 有关详细信息，请参阅本主题中的[启用远程管理](#bkmk_remote)。  
  
##  <a name="supported-versions-and-modes-of-analysis-services"></a><a name="bkmk_vers"></a> Analysis Services 的支持的版本和模式  
 目前，在 Windows Server 2008 R2、Windows Server 2008 SP1 或 Windows 7 上运行的任何版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services 均支持 Analysis Services PowerShell。  
  
 下表显示 Analysis Services PowerShell 在不同环境下的可用性。  
  
|上下文|PowerShell 功能可用性|  
|-------------|-------------------------------------|  
|多维实例和数据库|支持本地和远程管理。<br /><br /> 合并分区需要具有本地连接。|  
|表格实例和数据库|支持本地和远程管理。<br /><br /> 有关详细信息，请参阅8月2011博客，了解如何[使用 PowerShell 管理表格模型](https://go.microsoft.com/fwlink/?linkID=227685)。|  
|PowerPivot for SharePoint 实例和数据库|有限支持。 您可以使用 HTTP 连接和 SQLAS 提供程序查看实例和数据库信息。<br /><br /> 但是，不支持使用 cmdlet。 切勿使用 Analysis Services PowerShell 备份和还原内存中 PowerPivot 数据库，也不应添加或删除角色、处理数据或运行任意 XMLA 脚本。<br /><br /> 出于配置目的，PowerPivot for SharePoint 具有单独提供的内置 PowerShell 支持。 有关详细信息，请参阅[PowerShell Reference for PowerPivot for SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)。|  
|与本地多维数据集的本机连接<br /><br /> "Data Source = c:\backup\test.cub"|不支持。|  
|与 SharePoint 中的 BI 语义模型 (.bism) 连接文件的 HTTP 连接<br /><br /> "Data Source =http://server/shared_docs/name.bism"|不支持。|  
|与 PowerPivot 数据库的嵌入式连接<br /><br /> "Data Source = $Embedded $"|不支持。|  
|Analysis Services 存储过程中的本地服务器环境<br /><br /> "Data Source = *"|不支持。|  
  
##  <a name="authentication-requirements-and-security-considerations"></a><a name="bkmk_auth"></a>身份验证要求和安全注意事项  
 在连接到 Analysis Services 时，您必须使用 Windows 用户标识建立连接。 多数情况下都使用 Windows 集成安全性建立连接，由当前用户的标识设置执行服务器操作的安全上下文。 但是，在配置对 Analysis Services 的 HTTP 访问时，还可以使用其他身份验证方法。 本节介绍连接类型如何确定您可以使用的身份验证选项。  
  
 Analysis Services 连接可分为本机连接或 HTTP 连接。 本机连接是从客户端应用程序直接连接服务器。 在 PowerShell 会话中，PowerShell 客户端使用 OLE DB Provider for Analysis Services 直接连接 Analysis Services 实例。 始终使用 Windows 集成安全性建立本机连接，在此连接中 Analysis Services PowerShell 以当前用户身份执行操作。 Analysis Services 不支持模拟。 如果要以特定用户身份执行某一操作，您必须以该用户的身份启动 PowerShell 会话。  
  
 HTTP 连接是间接通过 IIS 建立的，该连接允许选择其他身份验证选项（如“基本身份验证”）来连接 Analysis Services 实例。 由于 IIS 支持模拟，您可以提供包含 IIS 建立连接时用来模拟的凭据的连接字符串。 若要提供凭据，可以使用-Credential 参数。  
  
 **在 PowerShell 中使用-Credential 参数**  
  
 -Credential 参数使用指定用户名和密码的 PSCredential 对象。 在 Analysis Services PowerShell 中，-Credential 参数适用于发出连接 Analysis Services 请求的 cmdlet，而不是在现有连接的上下文中运行的 cmdlet。 发出连接请求的 cmdlet 包括 Invoke-ASCmd、Backup-ASDatabase 和 Restore-ASDatabase。 对于这些 cmdlet，可以使用-Credential 参数，假定满足以下条件：  
  
1.  已配置服务器用于 HTTP 访问，这表示 IIS 在连接 Analysis Services 时会处理该连接、读取用户名和密码，并模拟用户身份。 有关详细信息，请参阅 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
2.  为 Analysis Services HTTP 访问创建的 IIS 虚拟目录配置用于“基本身份验证”。  
  
3.  凭据对象提供的用户名和密码解析为 Windows 用户标识。 Analysis Services 将此标识用作当前用户的标识。 如果该用户不是 Windows 用户，或是缺少足够的权限来执行请求的操作，该请求将失败。  
  
 若要创建凭据对象，您可以使用 Get-Credential cmdlet 从操作员处收集凭据。 随后可以在连接 Analysis Services 的命令中使用该凭据对象。 下面的示例演示了一种方法。 在此示例中，连接到配置为使用 HTTP 访问`SQLSERVER:\SQLAS\HTTP_DS`的本地实例（）。  
  
```powershell
$cred = Get-Credential adventureworks\dbadmin  
Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 在使用“基本身份验证”时，您应始终结合使用 HTTPS 和 SSL，以便通过加密连接发送用户名和密码。 有关详细信息，请参阅[在 iis 7.0 中配置安全套接字层](https://go.microsoft.com/fwlink/?linkID=184299)和[配置基本身份验证（IIS 7）](https://go.microsoft.com/fwlink/?LinkId=230776)。  
  
 请记住，您在 PowerShell 中提供的凭据、查询和命令将原样传递到传输层。 在脚本中包括敏感内容会增加恶意注入攻击的风险。  
  
 **提供作为 Microsoft.Secure.String 对象的密码**  
  
 某些操作（如备份与还原），支持当您在命令中提供提供密码时激活的加密选项。 提供密码即表示 Analysis Services 对备份文件进行加密或解密。 在 Analysis Services 中，此密码实例化为一个安全字符串对象。 下例演示了如何在运行时从操作员处收集密码。  
  
```powershell
$pwd = read-host -AsSecureString -Prompt "Password"  
$pwd -is [System.IDisposable]  
```  
  
 您可以备份和还原已加密的数据库文件，将 $pwd 变量传递给密码参数。 若要查看将此插图与其他 cmdlet 组合在一起的完整示例，请参阅[.asdatabase cmdlet](/powershell/module/sqlserver/backup-asdatabase)和[.asdatabase cmdlet](/powershell/module/sqlserver/restore-asdatabase)。
  
 作为后续步骤，需要从会话中删除该密码和变量。  
  
```powershell
$pwd.Dispose()  
Remove-Variable -Name pwd  
```  
  
##  <a name="analysis-services-powershell-tasks"></a><a name="bkmk_tasks"></a>Analysis Services PowerShell 任务  
 您可以从 Windows PowerShell Management Shell 或 Windows 命令提示符运行 Analysis Services PowerShell。 不支持从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 运行 Analysis Services PowerShell。  
  
 本节介绍使用 Analysis Services PowerShell 的常见任务。  
  
-   [加载 Analysis Services 提供程序和 Cmdlet](#bkmk_load)  
  
-   [启用远程管理](#bkmk_remote)  
  
-   [连接到 Analysis Services 对象](#bkmk_connect)  
  
-   [管理服务](#bkmk_admin)  
  
-   [获取有关 Analysis Services PowerShell 的帮助](#bkmk_help)  
  
###  <a name="load-the-analysis-services-provider-and-cmdlets"></a><a name="bkmk_load"></a>加载 Analysis Services 提供程序和 Cmdlet  
 Analysis Services 提供程序是 SQL Server 根提供程序的扩展插件，将在您导入 SQLPS 模块时提供。 Analysis Services cmdlet 同时加载；如果您想要使用这些 cmdlet，但不需要该提供程序，也可以单独加载它们。  
  
-   运行 Import-module cmdlet 可以加载包括所有 Analysis Services PowerShell 功能的 SQLPS。 如果您无法导入该模块，则可以出于加载该模块的目的，暂时将执行策略更改为不受限制。 有关详细信息，请参阅 [导入 SQLPS 模块](../../2014/database-engine/import-the-sqlps-module.md)。  
  
    ```powershell
    Import-Module "sqlps"  
    ```  
  
     或者，可以使用 `import-module "sqlps" -disablenamechecking` 禁止显示与未经批准的动词名称有关的警告。  
  
-   若要仅加载任务特定的 Analysis Services cmdlet，而不加载 Analysis Services 提供程序或 Invoke-ASCmd cmdlet，您可以在单独的操作中加载 SQLASCmdlets 模块。  
  
    ```powershell
    Import-Module "sqlascmdlets"  
    ```  
  
###  <a name="enable-remote-administration"></a><a name="bkmk_remote"></a>启用远程管理  
 您必须首先启用远程管理和文件共享，然后才能将 Analysis Services PowerShell 用于远程 Analysis Services 实例。 以下错误表明发生了防火墙配置问题： "RPC 服务器不可用。 (HRESULT 异常: 0x800706BA)”。  
  
1.  确认本地计算机和远程计算机都具有客户端和服务器工具的 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 版本。  
  
2.  在承载 Analysis Services 实例的远程服务器上，在 Windows 防火墙中打开 TCP 端口 2383。 如果您已将 Analysis Services 作为命名实例安装或者正在使用自定义端口，则该端口号将不同。 有关详细信息，请参阅 [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
3.  在远程服务器上，确认启动了以下服务：远程过程调用 (RPC) 服务、TCP/IP NetBIOS Helper 服务、Windows Management Instrumentation (WMI) 服务、Windows Remote Management (WS-Management) 服务。  
  
4.  在远程服务器上，启动组策略对象编辑器管理单元 (gpedit.msc)。  
  
5.  依次打开“计算机配置”、“管理模板”、“网络”、“网络连接”、“Windows 防火墙”和“域配置文件”。  
  
6.  双击 " **Windows 防火墙：允许入站远程管理例外**"，选择 "**已启用**"，然后单击 **"确定"**。  
  
7.  双击 " **Windows 防火墙：允许入站文件和打印机共享例外**"，选择 "**已启用**"，然后单击 **"确定"**。  
  
8.  在具有客户端工具的本地计算机上，使用以下 cmdlet 验证远程管理，并将实际的服务器名称替换为*远程服务器名称*占位符。 如果 Analysis Services 作为默认实例安装，则省略实例名称。 为使该命令正常执行，您必须在之前导入了 SQLPS 模块。  
  
    ```
    PS SQLSERVER:\> cd sqlas
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 在某些情况下，可能需要更多的配置。 您可能需要在远程服务器上键入以下命令，然后才能从其他计算机向其发出命令：  
  
```powershell
Enable-PSRemoting  
```  
  
  
###  <a name="connect-to-an-analysis-services-object"></a><a name="bkmk_connect"></a>连接到 Analysis Services 对象  
 Analysis Services PowerShell 提供程序支持在 Analysis Services 对象层次结构中导航和为正在运行的命令设置上下文。 该提供程序是可通过 SQLPS 模块获得的 SQLSERVER 根提供程序的扩展插件。 在您加载 SQLPS 模块后，可以导航该路径。  
  
 您可以连接到本地或远程实例，但某些 cmdlet 仅在本地实例上运行（即 merge-partition）。 您可以将本机连接或 HTTP 连接用于为 HTTP 访问配置的 Analysis Services 服务器。 下图说明用于本机和 HTTP 连接的导航路径。 下图说明用于本机和 HTTP 连接的导航路径。  
  
 **与 Analysis Services 的本机连接**  
  
 ![与 Analysis Services 的本机连接](media/ssas-powershell-nativeconnection.gif "与 Analysis Services 的本机连接")  
  
 下面的示例说明了如何使用本机连接导航对象层次结构。 通过该提供程序，您可以发出 `dir` 以便查看实例信息。 您可以使用 `cd` 查看该实例的对象。  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 您应该看到以下连接：程序集、数据库、角色和跟踪。 继续使用 `cd` 和 `dir`，您可以查看各连接的内容。  
  
 **HTTP 连接到 Analysis Services**  
  
 ![与 Analysis Services 的 HTTP 连接](media/ssas-powershell-httpconnection.gif "与 Analysis Services 的 HTTP 连接")  
  
 如果你使用本主题中的说明配置了用于 HTTP 访问的服务器，则 HTTP 连接很有用：[配置 Http 访问以对 Internet Information Services &#40;IIS&#41; 8.0 上的 Analysis Services](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 假设的服务器 URL http://localhost/olap/msmdpump.dll，连接可能如下所示：  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 您应该看到以下连接：程序集、数据库、角色和跟踪。 如果您无法看到这些连接的内容，则检查 OLAP 虚拟目录上的身份验证设置。 请确保禁用了匿名访问。 如果您在使用 Windows 身份验证，则应确保您的 Windows 用户帐户对该 Analysis Services 实例具有管理权限。  
  
###  <a name="administer-the-service"></a><a name="bkmk_admin"></a>管理服务  
 验证服务正在运行。 返回 SQL Server 服务的状态、名称和显示名称，包括 Analysis Services (MSSQLServerOLAPService) 和数据库引擎。  
  
```powershell
Get-Service mssql*  
```  
  
 返回与进程有关的属性，包括进程 ID、处理计数和内存使用情况：  
  
```powershell
Get-Process msmdsrv  
```  
  
 在您从管理员 shell 发出以下 cmdlet 时重新启动该服务：  
  
```powershell
Restart-Service mssqlserverolapservice  
```  
  
###  <a name="get-help-for-analysis-services-powershell"></a><a name="bkmk_help"></a>获取 Analysis Services PowerShell 的帮助  
 使用以下任何 cmdlet 可以验证 cmdlet 可用性并且获取有关服务、进程和对象的详细信息。  
  
1.  `Get-Help` 返回针对 Analysis Services cmdlet 的内置帮助，包括示例：  
  
    ```powershell
    Get-Help invoke-ascmd -Examples  
    ```  
  
2.  `Get-Command` 返回由 11 个 Analysis Services PowerShell cmdlet 组成的列表：  
  
    ```powershell
    Get-Command -module SQLASCmdlets  
    ```  
  
3.  `Get-Member` 返回服务或进程的属性或方法。  
  
    ```powershell
    Get-Service mssqlserverolapservice | Get-Member -Type Property  
    ```  
  
    ```powershell
    Get-Service mssqlserverolapservice | Get-Member -Type Method  
    ```  
  
    ```powershell
    Get-Process msmdsrv | Get-Member -Type Property  
    ```  
  
4.  `Get-Member` 也可用于返回对象的属性或方法（例如，针对服务器对象的 AMO 方法），使用 SQLAS 提供程序可以指定服务器实例。  
  
    ```
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | Get-Member -Type Method  
    ```  
  
5.  `Get-PSdrive` 返回当前安装的提供程序的列表。 如果您导入了 SQLPS 模块，将会在该列表中看到 `SQLServer` 提供程序（SQLAS 是 SQLServer 提供程序的一部分并且永远不会单独出现在该列表中）：  
  
    ```powershell
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [安装 SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [使用 PowerShell 管理表格模型（博客）](https://go.microsoft.com/fwlink/?linkID=227685)   
 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
