---
title: 用于 Reporting Services SharePoint 模式 PowerShell cmdlet |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e51aef3d9aa06790420cec9fab0d487a68563a4a
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658261"
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>用于 Reporting Services SharePoint 模式的 PowerShell cmdlet
  在安装 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式时，会安装 PowerShell cmdlet，以便支持 SharePoint 模式下的报表服务器。 这些 cmdlet 涵盖三个功能类别。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共享服务和代理的安装。  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序和关联代理的设置和管理。  
  
-   管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能，例如扩展插件和加密密钥。  
  
||  
|-|  
|[!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 **本主题包含以下内容：**  
  
-   [Cmdlet 摘要](#bkmk_cmdlet_sum)  
  
-   [共享服务和代理 Cmdlet](#bkmk_sharedservice_cmdlets)  
  
-   [服务应用程序和代理 Cmdlet](#bkmk_serviceapp_cmdlets)  
  
-   [Reporting Services 自定义功能 Cmdlet](#bkmk_ssrsfeatures_cmdlets)  
  
-   [基本示例](#bkmk_basic_samples)  
  
-   [详细的示例](#bkmk_detailedsamples)  
  
    -   [创建 Reporting Services 服务应用程序和代理](#bkmk_example_create_service_application)  
  
    -   [查看和更新 Reporting Services 传递扩展插件](#bkmk_example_delivery_extension)  
  
    -   [获取和设置 Reporting Service 应用程序数据库，例如数据库超时的属性](#bkmk_example_db_properties)  
  
    -   [列出 reporting services 数据扩展-SharePoint 模式](#bkmk_example_list_data_extensions)  
  
    -   [更改和列出订阅所有者](#bkmk_change_subscription_owner)  
  
##  <a name="bkmk_cmdlet_sum"></a> Cmdlet 摘要  
 若要运行 cmdlet，您需要打开 SharePoint Management Shell。 还可以使用 Microsoft Windows 附带的图形用户界面编辑器 **Windows PowerShell 集成脚本环境 (ISE)**。 有关详细信息，请参阅 [在 Windows Server 上启动 Windows PowerShell](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell)。 在以下 cmdlet 摘要中，对服务应用程序数据库，引用的数据库创建和使用的所有[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]服务应用程序。 这包括配置、警报和 temp 数据库。  
  
 如果您在键入 PowerShell 示例时看到类似以下内容的错误消息：  
  
-   Install-SPRSService:无法将字词 "Install-SPRSService" 识别为  
    cmdlet、函数、脚本文件或可运行程序的名称。 检查名称的拼写，如果包括路径，请验证路径是否正确并重试。  
  
 出现以下问题之一：  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式，因此未安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] cmdlet。  
  
-   您在 Windows PowerShell 或 Windows PowerShell ISE 而非 SharePoint Management Shell 中运行了 PowerShell 命令。 使用 SharePoint Management shell 或使用以下命令将 SharePoint 管理单元添加到 Windows PowerShell 窗口：  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 有关详细信息请参阅[使用 Windows PowerShell 管理 SharePoint 2013](https://technet.microsoft.com/library/ee806878.aspx) (https://technet.microsoft.com/library/ee806878.aspx)。  
  
#### <a name="to-open-the-sharepoint-management-shell-and-run-cmdlets"></a>打开 SharePoint Management Shell 并运行 cmdlet  
  
1.  单击 **“开始”** 按钮  
  
2.  单击 **“Microsoft SharePoint 产品”** 组。  
  
3.  单击 **“SharePoint Management Shell”**。  
  
 若要查看针对 cmdlet 的命令行帮助，请在 PowerShell 命令提示符处使用 PowerShell“Get-Help”命令。 例如：  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="bkmk_sharedservice_cmdlets"></a> 共享服务和代理 Cmdlet  
 下表包含用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共享服务的 PowerShell cmdlet。  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|安装并注册或卸载 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共享服务。 这只能在 SharePoint 模式下具有 SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装的计算机上进行。 对于安装，将发生两个操作：<br /><br /> 1)[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]服务安装在场中。<br /><br /> 2)[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]服务实例安装在当前计算机。<br /><br /> 对于卸载，将发生两个操作：<br />1)[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]从当前计算机上卸载服务。<br />2)[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]从场中卸载服务。<br /><br /> <br /><br /> 注意：如果场中存在安装了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务的任何其他计算机，或者场中仍有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序在运行，将显示一条警告消息。|  
|Install-SPRSServiceProxy|安装并注册（或卸载）SharePoint 场中的 Reporting Services 服务代理。|  
|Get-SPRSProxyUrl|获取用于访问 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务的 URL。|  
|Get-SPRSServiceApplicationServers|获取本地 SharePoint 场中包含 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 共享服务安装的所有服务器。 此 cmdlet 可用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 升级，以确定运行共享服务并因此需要升级的服务器。|  
  
###  <a name="bkmk_serviceapp_cmdlets"></a> 服务应用程序和代理 Cmdlet  
 下表包含用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序及其关联代理的 PowerShell cmdlet。  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|获取一个或多个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序对象。|  
|New-SPRSServiceApplication|创建一个新的 Reporting Services 服务应用程序及关联的数据库。<br /><br /> LogonType 参数:指定报表服务器是否使用 SSRS 应用程序池帐户或 SQL Server 登录名来访问报表服务器数据库。 该参数可以是下列值之一：<br /><br /> 0 Windows 身份验证<br /><br /> 1 SQL Server<br /><br /> 2 应用程序池帐户（默认值）|  
|Remove-SPRSServiceApplication|删除指定的 Reporting Services 服务应用程序。 此操作也将删除关联的数据库。|  
|Set-SPRSServiceApplication|编辑现有 Reporting Services 服务应用程序的属性。|  
|New-SPRSServiceApplicationProxy|创建新的 Reporting Services 服务应用程序代理。|  
|Get-SPRSServiceApplicationProxy|获取一个或多个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序代理。|  
|Dismount-SPRSDatabase|为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序卸除服务应用程序数据库。|  
|Remove-SPRSDatabase|为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序移除服务应用程序数据库。|  
|Set-SPRSDatabase|设置与 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序关联的数据库的属性。|  
|Mount-SPRSDatabase|装入 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序的数据库。|  
|New-SPRSDatabase|为指定的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序创建新的服务应用程序数据库。|  
|Get-SPRSDatabaseCreationScript|将数据库创建脚本输出到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序的屏幕。 然后，您可以在 SQL Server Management Studio 中运行此脚本。|  
|Get-SPRSDatabase|获取一个或多个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序数据库。 使用命令来获取服务应用程序数据库的 ID，以便使用 Set-SPRSDatabase cmdlet 来修改属性，例如 `querytimeout`。 请参阅本主题中的示例[获取和设置 Reporting Service 应用程序数据库的属性，例如数据库超时](#bkmk_example_db_properties)。|  
|Get-SPRSDatabaseRightsScript|将数据库权限脚本输出到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序的屏幕。 系统会提示所需的用户和数据库，然后返回您可以运行以修改权限的 Transact SQL。 然后，您可以在 SQL Server Management Studio 中运行此脚本。|  
|Get-SPRSDatabaseUpgradeScript|将数据库升级脚本输出到此屏幕。 该脚本将 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序数据库升级到当前 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装的数据库版本。|  
  
###  <a name="bkmk_ssrsfeatures_cmdlets"></a> Reporting Services 自定义功能 Cmdlet  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|为指定的 Reporting Services 服务应用程序更新加密密钥并且重新加密其数据。|  
|Restore-SPRSEncryptionKey|还原以前为 Reporting Services 服务应用程序备份的加密密钥。|  
|Remove-SPRSEncryptedData|为指定的 Reporting Services 服务应用程序删除加密数据。|  
|Backup-SPRSEncryptionKey|为指定的 Reporting Services 服务应用程序备份加密密钥。|  
|New-SPRSExtension|向 Reporting Services 服务应用程序注册新的扩展插件。|  
|Set-SPRSExtension|设置现有 Reporting Services 扩展插件的属性。|  
|Remove-SPRSExtension|从 Reporting Services 服务应用程序删除扩展插件。|  
|Get-SPRSExtension|获取一个或多个用于 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 扩展插件。<br /><br /> 有效值为<br /><br /> **传递**<br /><br /> **DeliveryUI**<br /><br /> **Render**<br /><br /> **Data**<br /><br /> **安全性**<br /><br /> **身份验证**<br /><br /> **EventProcessing**<br /><br /> **ReportItems**<br /><br /> **Designer**<br /><br /> **ReportItemDesigner**<br /><br /> **ReportItemConverter**<br /><br /> **ReportDefinitionCustomization**|  
|Get-SPRSSite|基于是否启用了“ReportingService”功能来获取 SharePoint 站点。 默认情况下，将返回启用“ReportingService”功能的站点。|  
  
##  <a name="bkmk_basic_samples"></a> 基本示例  
 返回在名称中包含“SPRS”的 cmdlet 的列表。 这将是 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] cmdlet 的完整列表。  
  
```  
Get-command -noun *SPRS*  
```  
  
 或者借助更详细的信息，传送到名为 commandlist.txt 的文本文件  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 安装 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 服务和服务代理。  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 启动 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 从 SharePoint Management Shell 键入以下命令，以便从日志文件中返回行的筛选后列表。 该命令将筛选包含“ssrscustomactionerror”的行。 此示例用于在安装 rssharepoint.msi 时查找创建的日志文件。  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
##  <a name="bkmk_detailedsamples"></a> 详细的示例  
 除以下示例之外，还可参阅 [Windows PowerShell 步骤脚本 1–4](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md#bkmk_full_script) 主题中的“Windows PowerShell 脚本”部分。  
  
###  <a name="bkmk_example_create_service_application"></a> 创建 Reporting Services 服务应用程序和代理  
 此示例脚本完成以下任务：  
  
1.  创建 Reporting Services 服务应用程序和代理。 该脚本假设应用程序池“My App Pool”已存在。  
  
2.  向默认代理组添加代理  
  
3.  授予服务应用对端口 80 Web 应用的内容数据库的访问权限。 该脚本假设网站"http://sitename"已存在。  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool "My App Pool"  
$serviceApp = New-SPRSServiceApplication "My RS Service App" -ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy -Name "My RS Service App Proxy" -ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application's content database.  
$webApp = Get-SPWebApplication "http://sitename"  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
###  <a name="bkmk_example_delivery_extension"></a> 查看和更新 Reporting Services 传递扩展插件  
 以下 PowerShell 脚本示例更新了名为 `My RS Service App`的服务应用程序的报表服务器电子邮件传递扩展插件的配置。 更新 SMTP 服务器 (`<email server name>`) 的值和 FROM 电子邮件别名 (`<your FROM email address>`)。  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = "<email server name>"  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 在上述示例中，如果您不知道服务应用程序的确切名称，则可重写第一个语句，以基于对部分名称的搜索获取服务应用程序。 例如：  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 下列脚本将返回名为“Reporting Services Application”的服务应用程序的报表服务器电子邮件传递扩展插件的当前配置值。 第一步将变量 $app 的值设置为具有“My RS Service App”名称的服务应用程序的对象。  
  
 第二个语句将获取变量 $app 中的服务应用程序对象的“报表服务器电子邮件”传递扩展插件，并选择配置 XML  
  
```  
$app=get-sprsserviceapplication -Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 你还可以将以上两个语句重写为一个：  
  
```  
get-sprsserviceapplication -Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="bkmk_example_db_properties"></a> 获取和设置 Reporting Service 应用程序数据库，例如数据库超时的属性  
 下面的示例首先返回数据库和属性列表，这样你可以确定你接下来为设置命令提供的数据库 GUID (ID)。 使用 `Get-SPRSDatabase | format-list`来获取完整的属性列表。  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 以下是输出的一个示例。 确定你想要修改的数据库的 ID，并在 SET cmdlet 中使用该ID。  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 若要验证是否已设置该值，请再次运行 GET cmdlet。  
  
```  
Get-SPRSDatabase -identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="bkmk_example_list_data_extensions"></a> 列出 reporting services 数据扩展-SharePoint 模式  
 以下示例遍历每个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 服务应用程序并列出它们每个的当前数据扩展插件。  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType "Data" | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **示例输出：**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
###  <a name="bkmk_change_subscription_owner"></a> 更改和列出订阅所有者  
 请参阅 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用 PowerShell 更改和列出 Reporting Services 订阅所有者并运行订阅](subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [清单：使用 PowerShell 验证 PowerPivot for SharePoint](../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
 [CodePlex SharePoint Management PowerShell 脚本](http://sharepointpsscripts.codeplex.com/)   
 [如何使用 PowerShell 管理 SSRS](https://curatedviews.cloudapp.net/13107/how-to-administer-ssrs-using-powershell)  
  
  
