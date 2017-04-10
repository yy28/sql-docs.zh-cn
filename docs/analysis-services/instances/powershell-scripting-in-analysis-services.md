---
title: "PowerShell scripting in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell scripting in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包括用于导航、管理和查询 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器、表格和多维对象的 PowerShell 组件：  
  
-   **SQLAS** 提供程序用于导航对象层次结构，该提供程序在你拥有任意 Analysis Services 本地实例时可用（与服务器模式无关）。  
  
-   **SQLASCMDLETS** 模块提供特定于任务的 cmdlet，例如备份、还原、处理，以及接受任何 ASSL/XMLA 或表格模型脚本语言 (TMSL) 查询或脚本输入文件的通用 [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)。  
  
 两个组件都实施了部分 Analysis Services 管理对象（[Microsoft.AnalysisServices 命名空间](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)）管理界面，提供 cmdlet 来管理和创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。  二者都是 SQL Server 的 **SQLPS** 根模块的扩展。 若要使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell 组件，请首先导入 **SQLPS**。 可以在 [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)中找到所有 cmdlet 的语法和示例。  有关如何在 PowerShell 中使用 AMO 类型来创建表格数据库的示例，请参阅 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)。  
  
##  <a name="bkmk_prereq"></a> 步骤 1：安装 PowerShell 组件  
 获取 PowerShell 组件的推荐方法是安装 SQL Server Management Studio (SSMS)。 这种方法提供 PowerShell 模块作为 SQL Server 和 Analysis Services 管理 (AMO) 的数据提供程序。 SSMS 也是一种工具，可以让你轻松地生成在 PowerShell 脚本中使用的 XMLA 和 TMSL 输入。  
  
 考虑安装 Analysis Services 的本地实例。 使用本地实例可以通过 **SQLAS** 提供程序来导航对象层次结构，即使你从来不用它来托管数据库。  
  
1.  转到  [Download SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx) （下载 SQL Server Management Studio）可获取最新版本的 Management Studio。 Management Studio 最新版本。 包括一个支持表格元数据对象定义的更新版 AMO，适用于在兼容级别 1200 创建的表格模型。  
  
2.  安装 Management Studio 以后，打开 PowerShell 窗口。 该窗口不必是管理员窗口。  
  
3.  输入 `Get-Module -ListAvailable`，确认 **SQLPS** 和 **SQLASCMDLETS** 模块显示在列表中。  
  
     你不会看到 **SQLAS**，除非你还安装了 Analysis Services 的本地实例（表格模式或多维模式）。  
  
4.  输入 `Get-Command -Module sqlascmdlets` 可生成一系列用于 Analysis Services 管理的 cmdlet。  
  
     即使**SQLASCMDLETS** 提供程序缺失，也可以使用 **SQLASCMDLETS** 。  
  
    -   [Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  Windows PowerShell 默认安装在 Windows 操作系统的较新版本上。 建议使用 4.0 或更高版本。  
  
## 步骤 2：加载启动交互式会话所需的组件  
 安装组件以后，加载这些组件即可启动交互式会话。  
  
1.  输入 `Import-Module sqlps -DisableNameChecking`。  
  
     加载 SQL Server PowerShell 组件，包括 Analysis Services 的组件，并禁止显示关于动词名称无效的警告。  
  
2.  输入 `sqlserver:`  
  
     你会看到提示符更改为 **PS SQLSERVER:\\>**。  
  
3.  如果 Analysis Services 安装在本地，则可导航对象层次结构。 输入 `cd sqlas` 打开 **SQLAS** 提供程序。  
  
4.  键入 `dir` 即可列出 Analysis Services 实例。 提供程序不区分表格实例和多维实例。  
  
## Permissions  
 交互式 PowerShell 会话在运行时，采用启动该会话的人员的安全标识。 大多数任务会要求启动会话的人也是 Analysis Services 服务器管理员。  
  
 应将计划的 PowerShell 任务视为无人参与操作。 大多数情况下，运行计划程序（例如 SQL Server 代理服务）的帐户可能需要是 Analysis Services 管理员（具体取决于任务）。  
  
 本地数据文件夹（例如默认的备份和数据目录）已配置了文件系统权限，因此本地实例可以在这些位置进行读取和写入操作。  
  
 远程管理（尤其是从尚未安装 Analysis Services 的客户端计算机进行远程管理）要求执行操作的远程 Analysis Services 服务器实例具有相应的文件系统权限，能够在还原期间读取文件或在备份期间写入文件。  
  
## 脚本输入文件：ASSL/XMLA 或 TMSL  
 如果你是使用 **invoke-ascmd** 来执行脚本，则在构造脚本时，应考虑服务器模式、数据库类型以及兼容级别。  
  
-   兼容级别为 1050-1103 的多维数据库和表格数据库会响应以 XMLA 编写的脚本（使用特定于 Analysis Services 对象定义的 ASSL 扩展）。  
  
-   基于 SQL Server 2016 的表格数据库（兼容级别为 1200）会响应 TMSL 脚本。  
  
 如果你要在同一 SQL Server 2016 实例上使用混合版本的表格模型，请记住使用正确的脚本。  
  
> [!NOTE]  
>  可以在 SQL Server Management Studio 中生成脚本，然后根据需要对其进行修改。 兼容级别为 1200 的表格数据库采用 TMSL 来编写脚本。 所有其他数据库采用 XMLA/ASSL 来编写脚本。 表格模式的 SQL Server 2016 实例支持这两种脚本语言。  
  
## 本地和远程管理  
 由于两个原因，通过 PowerShell 脚本和命令对 Analysis Services 进行本地管理更为容易：  
  
-   可以使用 **SQLAS** 提供程序来导航对象层次结构。  
  
-   允许 Analysis Services 从默认数据文件夹中针对特定任务（例如备份和还原任务）进行读取操作的文件权限已设置到位，前提是你将使用这些文件夹作为数据库位置，并将使用本地服务器实例进行操作。  
  
 管理远程实例需要额外的配置。 以下步骤假定你已完成 Management Studio 的安装步骤，但服务实例位于远程计算机上。 必须拥有 Analysis Services 服务器的管理员权限。  
  
 由于 Analysis Services 是远程服务，因此没有 **SQLAS** 提供程序可以在本地导航对象层次结构。 如果你要从本地文件夹而不是 Analysis Services 实例还原文件，则需创建共享并授予服务器对文件的读取访问权限。  
  
1.  打开管理员 PowerShell 窗口。  
  
2.  输入 `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  在文件资源管理器中，确保任何存储数据文件的文件夹都是共享文件夹，且 Analysis Services 实例具有对内容的读取权限。  
  
##  <a name="bkmk_vers"></a> Analysis Services 的支持的版本和模式  
 下表显示 Analysis Services PowerShell 在不同环境下的可用性。  
  
|Context|PowerShell 功能可用性|  
|-------------|-------------------------------------|  
|多维实例和数据库|支持本地和远程管理。<br /><br /> 合并分区需要具有本地连接。|  
|表格实例和数据库|支持在所有兼容级别进行本地和远程管理。<br /><br /> SQLAS cmdlet，适用于表格模型，兼容级别为 1200，使用表格模型脚本语言 (TMSL)，采用 JSON 而非 XMLA 格式。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 实例和数据库|有限支持。 您可以使用 HTTP 连接和 SQLAS 提供程序查看实例和数据库信息。<br /><br /> 但是，不支持使用 cmdlet。 不能使用 Analysis Services PowerShell 备份和还原内存中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库，也不应添加或删除角色、处理数据或运行任意 XMLA 脚本。<br /><br /> 出于配置目的，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 具有单独提供的内置 PowerShell 支持。 有关详细信息，请参阅[针对 Power Pivot for SharePoint 的 PowerShell 参考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)。|  
|与本地多维数据集的本机连接<br /><br /> “Data Source=c:\backup\test.cub”|不提供支持。|  
|与 SharePoint 中的 BI 语义模型 (.bism) 连接文件的 HTTP 连接<br /><br /> “Data Source=http://server/shared_docs/name.bism”|不提供支持。|  
|与 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库的嵌入式连接<br /><br /> “Data Source=$Embedded$”|不提供支持。|  
|Analysis Services 存储过程中的本地服务器环境<br /><br /> “Data Source=*”|不提供支持。|  
  
## PowerShell 服务器管理任务示例  
 **列出服务器属性**  
  
 以多种方式公开服务器属性。  如果你熟悉在 msmdsrv. ini 或 Management Studio 的属性页中公开的属性，则会在下面的示例中看到，这些属性实际上是从不同对象返回的。  
  
 此脚本加载 AMO 服务器对象。 若需完全限定的属性名，则可运行此脚本以返回该列表。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 此脚本返回实例级别的属性和方法。 在此列表中，你可以读取 **ServerMode**、 **Version**、 **ProductName**或 **ProductLevel**这样的值。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **获取服务器模式**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **获取默认兼容级别**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **获取数据库列表**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **更改端口号**  
  
 此脚本可以为命名实例创建对象、声明端口、设置端口、更新服务器实例、断开对象的连接，以及重新启动服务。 可以通过打开新的连接并返回端口来进行验证。  
  
 还可以在 Management Studio 中的 msmdsrv.ini 文件或服务器的通用属性页对端口进行验证。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## 另请参阅  
 [向 Analysis Services 实例授予服务器管理员权限](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [安装 SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [使用 PowerShell 管理表格模型](http://go.microsoft.com/fwlink/?linkID=227685)   
 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  