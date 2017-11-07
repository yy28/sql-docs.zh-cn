---
title: "清单： 使用 PowerShell 验证 Power Pivot for SharePoint |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa577404c035753f7173546aff32fe0f8d1ee7a1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="checklist-use-powershell-to-verify-power-pivot-for-sharepoint"></a>核对清单：使用 PowerShell 验证 Power Pivot for SharePoint
  若非通过可靠的验证测试确认服务和数据运行正常， [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 安装或恢复操作就不算完成。 在本文中，我们将介绍如何使用 Windows PowerShell 执行这些步骤。 我们将每个步骤作为一个章节，方便您跳转到特定的任务。 例如，如果您需要安排服务应用程序和内容数据库的维护或备份操作，则可运行此主题中 [“数据库”](#bkmk_databases) 章节的脚本，以验证服务应用程序和内容数据库的名称。  
  
|||  
|-|-|  
|![PowerShell 相关内容](../../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相关内容")|本主题下方包含了一个完整的 PowerShell 脚本。 您可以使用此完整脚本作为起点，构建用于审计 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 完整部署的自定义脚本。|  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **本主题内容**：下面目录中带字母的项目对应于关系图区域。 关系图说明  
  
|||  
|-|-|  
|[准备 PowerShell 环境](#bkmk_prerequisites)<br /><br /> [症状和建议操作](#bkmk_symptoms)<br /><br /> **(A)** [Analysis Services Windows 服务](#bkmk_windows_service)<br /><br /> **(B)** [PowerPivotSystemService 和 PowerPivotEngineSerivce](#bkmk_engine_and_system_service)<br /><br /> **(C)** [Power Pivot 服务应用程序和代理](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [“数据库”](#bkmk_databases)<br /><br /> [SharePoint 功能](#bkmk_features)<br /><br /> [计时器作业](#bkmk_timer_jobs)<br /><br /> [运行状况规则](#bkmk_health_rules)<br /><br /> **(E)** [Windows 和 ULS 日志](#bkmk_logs)<br /><br /> [MSOLAP 访问接口](#bkmk_msolap)<br /><br /> [ADOMD.Net 客户端库](#bkmk_adomd)<br /><br /> [运行状况数据收集规则](#bkmk_health_collection)<br /><br /> [解决方案](#bkmk_solutions)<br /><br /> [手动验证步骤](#bkmk_manual)<br /><br /> [更多资源](#bkmk_more_resources)<br /><br /> [完整的 PowerShell 脚本](#bkmk_full_script)|![powershell 验证 powerpivot](../../../analysis-services/instances/install-windows/media/ssas-powershell-component-verification.png "powershell 验证 powerpivot")|  
  
##  <a name="bkmk_prerequisites"></a> 准备 PowerShell 环境  
 本章节的步骤旨在准备 PowerShell 环境。 这些不一定是必需步骤，具体视脚本环境的当前配置方式而定。  
  
 **PowerShell 权限**  
  
 以 **管理员权限**打开 Powershell 窗口或 PowerShell ISE（集成脚本环境）。 如果您不具备管理员权限，则在运行命令时，可能会显示类似以下内容的错误消息：  
  
 Get-SPLogEvent：需要拥有计算机的**管理员权限**才能运行此 cmdlet。  
  
 **SharePoint 和 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)]** 模块  
  
 在运行 SharePoint 相关 cmdlet 时，如果显示类似以下内容的错误消息，请运行 Add-PSSnapin 命令：  
  
 无法将“Get-PowerPivotSystemService”项 **识别为 cmdlet**、函数、脚本文件或可运行程序的名称。 检查名称的拼写，如果包括路径，请验证路径是否正确并重试。  
  
```  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
```  
  
 **Windows PowerShell**  
  
 有关 PowerShell ISE 的详细信息，请参阅 [Windows PowerShell ISE 简介](http://technet.microsoft.com/library/dd315244.aspx) 和 [使用 Windows PowerShell 管理 SharePoint 2013](http://technet.microsoft.com/library/ee806878\(v=office.15\).aspx)。  
  
|||  
|-|-|  
|![在 sharepoint 常规应用程序集中的 powerpivot](../../../analysis-services/instances/install-windows/media/ssas-powerpivot-logo.png "sharepoint 常规应用程序集中的 powerpivot")|借助 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理面板，您可以在管理中心有选择地验证大多数组件。 要在“管理中心”打开该面板，请单击“常规应用程序设置” ，然后单击 **中的“管理面板”****[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]**。 有关该面板的详细信息，请参阅 [Power Pivot Management Dashboard and Usage Data](../../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)。|  
  
##  <a name="bkmk_symptoms"></a> 症状和建议操作  
 下表列出了症状或问题，以及本主题的建议章节（旨在帮助您解决问题）。  
  
|故障现象|参阅章节|  
|-------------|-----------------|  
|未运行数据刷新|请参阅 [计时器作业](#bkmk_timer_jobs) 章节，并验证 **联机 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 数据刷新计时器作业** 是否处于联机状态。|  
|管理面板数据陈旧|请参阅 [计时器作业](#bkmk_timer_jobs) 章节，并验证 **“管理面板处理计时器作业”** 是否处于联机状态。|  
|管理面板的某些部分|如果你将 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 安装到具有管理中心拓扑但没有 Excel Services 或 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 的场中，并且希望对 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 管理面板中的内置报表具有完全访问权限，则必须下载和安装 Microsoft ADOMD.NET 客户端库。 该面板中的某些报表将使用 ADOMD.NET 来访问内部数据，内部数据可提供有关 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 查询处理和场中服务器运行状况的报告数据。 请参阅 [ADOMD.Net 客户端库](#bkmk_adomd) 章节和 [在运行管理中心的 Web 前端服务器上安装 ADOMD.NET](http://msdn.microsoft.com/en-us/c2372180-e847-4cdb-b267-4befac3faf7e)主题。|  
  
##  <a name="bkmk_windows_service"></a> Analysis Services Windows 服务  
 本章节中的脚本用于验证 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] SharePoint 模式下的实例。 验证服务正在 **运行**。  
  
```  
get-service | select name, displayname, status | where {$_.Name -eq "msolap`$powerpivot"} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
Name              DisplayName                                Status  
----              -----------                                ------  
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running  
```  
  
##  <a name="bkmk_engine_and_system_service"></a> PowerPivotSystemService 和 PowerPivotEngineSerivce  
 本章节中的脚本用于验证 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 系统服务。 用于 SharePoint 2013 部署的系统服务有一个，用于 SharePoint 2010 部署的服务有两个。  
  
 **PowerPivotSystemService**  
  
 验证状态是否为 **联机**。  
  
```  
Get-PowerPivotSystemService | select typename, status, applications, farm | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
TypeName                                  Status Applications                             Farm  
--------                                  ------ ------------                             ----  
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c  
```  
  
 **PowerPivotEngineSerivce**  
  
> [!NOTE]  
>  如果您使用的是 SharePoint 2013，请**跳过该脚本** 。 PowerPivotEngineService 不是 SharePoint 2013 部署的一部分。 如果你在 SharePoint 2013 上运行 Get-PowerPivotEngineService cmdlet，那么你将看到类似以下内容的错误消息。 即使您已运行了本主题先决条件中说明的 Add-PSSnapin 命令，仍会返回该错误消息。  
>   
>  无法将“Get-PowerPivotEngineService”项识别为 cmdlet 的名称  
  
 在 SharePoint 2010 部署中，请验证状态是否为 **联机**。  
  
```  
Get-PowerPivotEngineService | select typename, status, name, instances, farm | format-table -property * -autosize | out-default   
```  
  
 **示例输出**  
  
```  
TypeName  : SQL Server Analysis Services  
Status    : Online  
Name      : MSOLAP$POWERPIVOT  
Instances : {POWERPIVOT}  
Farm      : SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_powerpivot_service_application"></a> Power Pivot 服务应用程序和代理  
 验证状态是否为 **联机**。 Excel Services 应用程序不使用服务应用程序数据库，因此，cmdlet 不返回数据库名称。 记下 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 服务应用程序使用的数据库，以便在本主题后面的数据库章节中验证此数据库是否联机。  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 和 Excel Service 应用程序**  
  
 对于 SharePoint 2010 部署，验证状态是否为 **联机**。  
  
```  
Get-PowerPivotServiceApplication | select typename,name, status, unattendedaccount, applicationpool, farm, database  
Get-SPExcelServiceApplication | select typename, DisplayName, status  
```  
  
 **示例输出**  
  
```  
TypeName          : PowerPivot Service Application  
Name              : PowerPivotServiceApplication1  
Status            : Online  
UnattendedAccount : PowerPivotUnattendedAccount  
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp  
Farm              : SPFarm Name=SharePoint_Config  
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a  
  
TypeName    : Excel Services Application Web Service Application  
DisplayName : Excel Services Application  
Status      : Online  
```  
  
 **服务应用程序池**  
  
> [!NOTE]  
>  下面的代码示例首先返回默认 [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 服务应用程序的 applicationpool 属性。 系统从此字符串解析出名称，并用其获取应用程序池对象的状态。  
>   
>  验证状态是否为 **联机**。 如果状态为未联机或您在浏览 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 站点时遇到“http 错误”，请验证 IIS 应用程序池中的标识凭据是否仍正确。 IIS 池名称将为 Get-SPServiceApplicationPool 命令返回的 ID 属性的值。  
  
```  
$poolname=[string](Get-PowerPivotServiceApplication | select -property applicationpool)  
$position=$poolname.lastindexof("=")  
$poolname=$poolname.substring($position+1)  
$poolname=$poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | select name, status, processaccountname, id | where {$_.Name -eq $poolname} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
Name                           Status ProcessAccountName Id  
----                           ------ ------------------ -------   
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea  
```  
  
 ![请注意](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")还可以在管理中心页上验证了应用程序池**管理服务应用程序**。 单击服务应用程序的名称，然后单击功能区中的 **“属性”** 。  
  
 **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 和 Excel Service 应用程序代理**  
  
 验证状态是否为 **联机**。  
  
```  
Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
TypeName                                                 Status UnattendedAccount           DisplayName  
--------                                                 ------ -----------------           -----------  
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1  
Excel Services Application Web Service Application Proxy Online                             Excel Services Application  
```  
  
##  <a name="bkmk_databases"></a> “数据库”  
 下面的脚本返回服务应用程序数据库和所有内容数据库的状态。 验证状态是否为 **联机**。  
  
```  
Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*”} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
Name                                                                       Status Server                  TypeName   
----                                                                       ------ ------                  --------   
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase  
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database   
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database  
  
```  
  
##  <a name="bkmk_features"></a> SharePoint 功能  
 验证站点、Web 和场功能是否联机。  
  
```  
Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like “*powerpivot*”} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
DisplayName     Status Scope Farm                           
-----------     ------ ----- ----                           
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config  
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config  
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_timer_jobs"></a> 计时器作业  
 验证计时器作业是否 **“联机”**。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] EngineService 未安装在 SharePoint 2013 上，因此，此脚本不会列出 SharePoint 2013 部署中的 EngineService 计时器作业。  
  
```  
Get-SPTimerJob | where {$_.service -like "*power*" -or $_.service -like "*mid*"} | select status, displayname, LastRunTime, service | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
  
      Status DisplayName                                                                          LastRunTime          Service                               
------ -----------                                                                          -----------          -------                               
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT  
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService  
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService  
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService  
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService  
```  
  
##  <a name="bkmk_health_rules"></a> 运行状况规则  
 SharePoint 2013 部署中包含少量规则。 有关各个 SharePoint 环境规则的完整列表和规则使用方法的说明，请参阅 [配置 Power Pivot 运行状况规则](../../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)。  
  
```  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like “*power*”}  | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
Name                          Enabled Summary  
----                          ------- -------           
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled  
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.  
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.  
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash  
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.  
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin  
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.  
```  
  
##  <a name="bkmk_logs"></a> Windows 和 ULS 日志  
 **Windows 事件日志**  
  
 下面的命令将在 Windows 事件日志中搜索与 SharePoint 模式下的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例相关的事件。 有关禁用事件或更改的事件级别的信息，请参阅[配置和查看 SharePoint 日志文件和诊断日志记录 &#40;Power Pivot for SharePoint &#41;](../../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)
 
 **服务名称：** MSOLAP$POWERPIVOT  
  
 **Windows 服务中的显示名称：** SQL Server Analysis Services (POWERPIVOT)  
  
```  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
TimeGenerated           EntryType Source            Message  
-------------           --------- ------            -------  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.  
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.  
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
```  
  
 **SharePoint ULS 日志，最近 48 小时**  
  
 下面的命令将从 ULS 日志返回最近 48 小时内创建的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 消息。 根据需要调整 addhours 参数。  
  
```  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | select timestamp, area, category, eventid,level, message| format-table -property * -autosize | out-default  
```  
  
 下面的命令变体只返回 **数据刷新** 类别的日志事件。  
  
```  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
```  
  
 **示例输出**  
  
```  
Timestamp   : 4/14/2014 7:15:01 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 43  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : The following error occured when working with the service application, Default PowerPivot Service Application. Skipping the service application..  
  
Timestamp   : 4/14/2014 7:15:02 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 99  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to   
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout.   
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the   
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The   
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at   
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...  
```  
  
##  <a name="bkmk_msolap"></a> MSOLAP 访问接口  
 验证 MSOLAP 访问接口。 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 需要 MSOLAP.5。  
  
```  
$excelApp=Get-SPExcelServiceApplication  
get-spexceldataprovider -ExcelServiceApplication $excelApp |select providerid,providertype,description | where {$_.providerid -like “msolap*” } | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
ProviderId ProviderType Description  
---------- ------------ -----------  
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services       
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0   
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0  
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0  
```  
  
 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) 和 [将 MSOLAP.5 添加为 Excel Services 中的受信任数据提供程序](http://technet.microsoft.com/library/hh758436.aspx)。  
  
##  <a name="bkmk_adomd"></a> ADOMD.Net 客户端库  
  
```  
get-wmiobject -class win32_product | Where-Object {$_.name -like "*ado*"} | select name, version, vendor | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
name                                                  version      vendor  
----                                                  -------      ------  
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation  
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation  
```  
  
 有关详细信息，请参阅 [在运行管理中心的 Web 前端服务器上安装 ADOMD.NET](http://msdn.microsoft.com/en-us/c2372180-e847-4cdb-b267-4befac3faf7e)。  
  
##  <a name="bkmk_health_collection"></a> 运行状况数据收集规则  
 验证 **“状态”** 是否联机，以及 **“已启用”** 是否为 True。  
  
```  
get-spusagedefinition | select name, status, enabled, tablename, DaysToKeepDetailedData | where {$_.name -like "powerpivot*"} | format-table -property * -autosize | out-default  
```  
  
 **示例输出**  
  
```  
Name                         Status Enabled TableName                   DaysToKeepDetailedData  
----                         ------ ------- ---------                   ----------------------  
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14  
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14  
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14  
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14  
```  
  
 有关详细信息，请参阅 [Power Pivot Usage Data Collection](../../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)。  
  
##  <a name="bkmk_solutions"></a> 解决方案  
 如果其他组件联机，则可跳过方案验证的验证。 但是，如果缺少运行状况规则，则需验证这两个解决方案是否存在，并验证两个 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 解决方案是否为 **“联机”** 且 **“已部署”**。  
  
```  
get-spsolution | select name, status, deployed, DeploymentState, DeployedServers | where {$_.Name -like “*powerpivot*”} | format-table -property * -autosize | out-default  
```  
  
 **示例输出 SharePoint 2013**  
  
```  
Name                                 Status Deployed        DeploymentState DeployedServers  
----                                 ------ --------        --------------- ---------------  
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}  
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}  
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}  
```  
  
 **示例输出 SharePoint 2010**  
  
```  
Name                 Status Deployed        DeploymentState DeployedServers   
----                 ------ --------        --------------- ---------------   
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}  
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}  
```  
  
 有关如何部署 SharePoint 解决方案的详细信息，请参阅 [部署解决方案包 (SharePoint Server 2010)](http://technet.microsoft.com/library/cc262995\(v=office.14\).aspx)。  
  
##  <a name="bkmk_manual"></a> 手动验证步骤  
 本章节介绍无法借由 PowerShell cmdlet 完成的验证步骤。  
  
 **计划的数据刷新：** 将工作簿的刷新计划配置为 **“也尽快刷新”**。  有关详细信息，请参阅[计划数据刷新和不支持 Windows 身份验证的数据源 (Power Pivot for SharePoint)](../../../analysis-services/power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md) 中的“验证数据刷新”部分。  
  
##  <a name="bkmk_more_resources"></a> 更多资源  
 [Windows PowerShell 中的 Web 服务器 (IIS) 管理 Cmdlet](http://technet.microsoft.com/library/ee790599.aspx)。  
  
 [用于检查 SharePoint 中服务、IIS 站点和应用程序池状态的 PowerShell](http://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0)。  
  
 [Windows PowerShell for SharePoint 2013 参考](http://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)  
  
 [Windows PowerShell for SharePoint Foundation 2010 参考](http://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)  
  
 [使用 Windows PowerShell 管理 Excel Services (SharePoint Server 2010)](http://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)  
  
 [查看和读取 SQL Server 安装程序日志文件](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
 [使用 Get-EvenLog cmdlet](http://technet.microsoft.com/library/ee176846.aspx)  
  
##  <a name="bkmk_full_script"></a> 完整的 PowerShell 脚本  
 下面的脚本包含上述章节的所有命令。 此脚本以本主题中显示的顺序运行命令。 此脚本包含本主题中提到的某些可选命令变体，方便您在需要其他筛选条件时使用。 变体已用注释字符 (#) 禁用。 此脚本还包含某些验证 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式的语句。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 语句已用注释字符 (#) 禁用。  
  
```  
# This script audits services related to PowerPivot for SharePoint  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
  
Write-Host  "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell –EA 0  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Analysis Services Windows Service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-service | select name, displayname, status | where {$_.Name -eq "msolap`$powerpivot"} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivotEngineSerivce and PowerPivotSystemService"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
Get-PowerPivotSystemService | select typename, status, applications, farm | format-table -property * -autosize | out-default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
Get-PowerPivotEngineService | select typename, status, name, instances, farm | format-table -property * -autosize | out-default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
#Write-Host ""  
#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"  
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel*” -or $_.TypeName -like “*Analysis Services*”} | format-table -property * -autosize | out-default  
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance  
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-PowerPivotServiceApplication | select typename,name, status, unattendedaccount, applicationpool, farm, database   
Get-SPExcelServiceApplication | select typename,  DisplayName, status   
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
# the following assumes there is only 1 PowerPivot Service Application, and returns that applicaitons pool name.  if you have more than one, use the 2nd version  
$poolname=[string](Get-PowerPivotServiceApplication | select -property applicationpool)  
$position=$poolname.lastindexof("=")  
$poolname=$poolname.substring($position+1)  
$poolname=$poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | select name, status, processaccountname, id | where {$_.Name -eq $poolname} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like “*powerpivot*” -or $_.TypeName -like “*Reporting Services*” -or $_.TypeName -like “*excel services*”} | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "DATABASES"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*”} | format-table -property * -autosize | out-default  
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq “content database” -or $_.TypeName -like “*Gemini*” -or $_.TypeName -like “*ReportingServices*”}   
  
#Write-Host ""  
Write-Host -ForegroundColor Green "features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPFeature | select displayname, status, scope, farm| where {$_.displayName -like “*powerpivot*”} | format-table -property * -autosize | out-default  
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like “*powerpivot*” -or $_.displayName -like “*ReportServer*”}  | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPTimerJob | where {$_.service -like "*power*" -or $_.service -like "*mid*"} | select status, displayname, LastRunTime, service | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "health rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPHealthAnalysisRule | select name, enabled, summary | where {$_.summary -like “*power*”}  | format-table -property * -autosize | out-default  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
#The following is the same command but with the Inforamtion events filtered out.  
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "ULS Log data"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | select timestamp, area, category, eventid,level, correlation, message| format-table -property * -autosize | out-default  
#the following example filters for the category 'data refresh'  
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
$excelApp=Get-SPExcelServiceApplication  
get-spexceldataprovider -ExcelServiceApplication $excelApp |select providerid,providertype,description | where {$_.providerid -like “msolap*” } | format-table -property * -autosize | out-default  
  
Write-Host -ForegroundColor Green "ADOMD.net client library"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-wmiobject -class win32_product | Where-Object {$_.name -like "*ado*"} | select name, version, vendor | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "Usage Data Rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-spusagedefinition | select name, status, enabled, tablename, DaysToKeepDetailedData | where {$_.name -like "powerpivot*"} | format-table -property * -autosize | out-default  
  
Write-Host -ForegroundColor Green "Solutions"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
get-spsolution | select name, status, deployed, DeploymentState, DeployedServers | where {$_.Name -like “*powerpivot*”} | format-table -property * -autosize | out-default  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime   
write-host -foregroundcolor DarkGray EndTime $time  
  
```  
  
  

