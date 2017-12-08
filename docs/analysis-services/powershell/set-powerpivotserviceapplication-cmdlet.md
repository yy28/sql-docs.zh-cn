---
title: "集 PowerPivotServiceApplication cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 16d10e2d-d7e1-40f1-bc9d-a4e10c61af95
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0def855b93ce209aa923fd57e60d01c142a7fd0d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="set-powerpivotserviceapplication-cmdlet"></a>Set-PowerPivotServiceApplication cmdlet
  
 [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)] 

  设置 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的属性。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
 **适用范围：** SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>语法  
  
```  
Set-PowerPivotServiceApplication [-Identity] <SPGeminiServiceApplicationPipeBind> [-AdministrationConnectionPoolSize <int>] [-AllowCustomWindowsCredentials] [-BusinessHoursEndTime <string>] [-BusinessHoursStartTime <string>] [-CachedDatabaseholdLimit <int>] [-Confirm <switch>] [-ConnectionPoolSize <int>] [-ConnectionPoolTimeout <int>] [-DataLoadTimeout <int>] [-DataRefreshFailureThreshold <int>] [-DataRefreshInactiveWorkbooksThreshold <int>] [-DataRefreshMaxHistory <int>] [-HealthBasedAllocation <switch>] [-LoadsToConnectionsRatioCollectionInterval <int>] [-LoadsToConnectionsRatioLimit <int>] [-MemoryDatabaseHoldLimit <int>] [-QueryReportingInterval <int>] [-RoundRobinAllocation <switch>] [-UnattendedAccount <string>] [-UsageDataRetentionPeriod <int>] [-UsageExpectedResponseUpperLimit <int>] [-UsageLongResponseUpperLimit <int>] [-UsageQuickResponseUpperLimit <int>] [-UsageTrivialResponseUpperLimit <int>] [-UsageUpdateDayLimit <int>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Set-PowerPivotServiceApplication cmdlet 更新场中 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序的属性。 Identity 参数是必需的。 您必须提供要更新其属性的服务应用程序的 GUID。  
  
 若要验证所做的更改，请运行以下 cmdlet: Get PowerPivotServiceApplication-标识\<GUID > | 格式列表。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>标识\<SPGeminiServiceApplicationPipeBind >  
 指定要更新的服务应用程序。 该类型必须是有效的 GUID 或有效的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序对象的实例。 您可以使用 Get-PowerPivotServiceApplication 返回对象的实例。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|true|  
|接受通配符？|false|  
  
### <a name="-administrationconnectionpoolsize-int"></a>-AdministrationConnectionPoolSize \<int >  
 指定连接池中为与 Analysis Services 的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务连接而创建的打开的连接数目。 每个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务实例都打开与同一计算机上的 Analysis Services 实例的单独管理连接。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务创建一个单独的池以便出于检查空闲连接和监视服务器运行状况的目的而重用管理连接。 默认值为 200 个连接。 有效值为 -1（无限制）、0（禁用管理连接池）或 1 到 100。 如果您选择 0，将重新创建每个连接。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|200|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-allowcustomwindowscredentials-switchparameter"></a>-AllowCustomWindowsCredentials [\<SwitchParameter >]  
 指定计划所有者是否可以输入任意 Windows 凭据以便运行数据刷新计划。 如果选中此复选框， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序将为每组存储凭据都创建和管理目标应用程序。 默认设置为 true。 若要关闭此功能，请设置 AllowCustomWindowsCredentials:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-businesshoursendtime-string"></a>-BusinessHoursEndTime\<字符串 >  
 指定用于定义工作日的小时范围的结束时间。 数据刷新计划可以在下班后运行，以便选取在正常工作时间中生成的事务数据。 默认值为 8:00 p.m.  有效值在引号中指定，并且采用 a.m. 或 p.m. 时钟时间（例如，"08:00PM"）。 小时必须介于 1 和 12 之间。 分钟必须介于 1 和 59 之间。  
  
 若要指定工作日的完整小时范围，必须一起设置 BusinessHoursStartTime 和 BusinessHoursEndTime。 这两个参数定义构成工作日的小时间隔。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|8 PM|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-businesshoursstarttime-string"></a>-BusinessHoursStartTime\<字符串 >  
 指定用于定义工作日的小时范围的开始时间。 数据刷新计划可以在下班后运行，以便选取在正常工作时间中生成的事务数据。 默认值为 4:00 a.m.  有效值在引号中指定，并且采用 a.m. 或 p.m. 时钟时间（例如，"04:00AM"）。 小时必须介于 1 和 12 之间。 分钟必须介于 1 和 59 之间。  
  
 若要指定工作日的完整小时范围，必须一起设置 BusinessHoursStartTime 和 BusinessHoursEndTime。 这两个参数定义构成工作日的小时间隔。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|4 AM|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-cacheddatabaseholdlimit-int"></a>-CachedDatabaseholdLimit \<int >  
 指定非活动数据库在文件系统上保留多少小时后，将会从内存中卸载。 默认值为 120 小时。 清除作业将使用此设置来确定要删除的文件。 168 小时（48 小时在内存中，120 小时在缓存中）处于非活动状态的所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据库都将由清除作业从磁盘中删除。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|120|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-confirm-switch"></a>确认\<切换 >  
 在执行命令前提示您进行确认。 默认情况下将启用该值。 若要在命令中跳过确认响应，请在命令中指定 Confirm:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-connectionpoolsize-int"></a>-ConnectionPoolSize \<int >  
 指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务将在单独的连接池中为各 SharePoint 用户、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据集和版本组合创建的空闲连接的最大数目。 默认值为 1000 个空闲连接。 有效值为 -1（无限制）、0（禁用用户连接池）或 1 到 10000。 这些连接池使服务能够更有效地支持由同一用户建立的与相同只读数据的持续连接。 如果您禁用了连接池，将重新创建每个连接。 请注意，更改对连接池大小的限制（包括将其设置为 0）不会导致删除连接。 连接池存在的目的是减少连接数据时需要等待的时间。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务将永远不会拒绝基于连接池设置的连接。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|1000|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-connectionpooltimeout-int"></a>-ConnectionPoolTimeout \<int >  
 指定空闲数据连接将保持打开状态的分钟数。 默认值为 1800 秒（或 30 分钟）。 在此期间，对于来自相同 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据的同一 SharePoint 用户的只读请求， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序将重用空闲数据连接。 如果在指定的时段中没有收到针对该数据的进一步的请求，则从池中删除该连接。 有效值为 1 至 3600 秒。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|1800|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-dataloadtimeout-int"></a>-DataLoadTimeout \<int >  
 指定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务应用程序等待来自它将加载数据请求转发到的 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 实例的响应的时间长度。 因为非常大的数据集需要花时间在线路上移动，所以必须确保 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服务实例有充裕的时间检索 Excel 工作簿并将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据移到 Analysis Services 实例以便进行查询处理。 默认值为 1800 秒（或 30 分钟）。 有效值为 1 到 3600 秒。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|1800|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-datarefreshfailurethreshold-int"></a>-DataRefreshFailureThreshold \<int >  
 指定经过多少次连续失败，将会禁用计划。 默认值为 10。 您还可以输入 0，永远不会由于刷新失败而禁用计划。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|10|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-datarefreshinactiveworkbooksthreshold-int"></a>-DataRefreshInactiveWorkbooksThreshold \<int >  
 指定经过了多少个数据刷新周期后就将禁用计划，或者输入 0，以便永远不会由于不活动而禁用计划。 默认值为 10 个周期。  
  
 如果对于多个数据刷新周期都没有连接事件，则认为工作簿不活动。 每次触发数据刷新操作（通过计划或“立即运行”操作触发）时都会对数据刷新周期计数，而与该操作是成功还是失败无关。 如果经过了一定数目的周期（默认为 10）且没有针对该工作簿的连接请求，则数据刷新计划将由于不活动而被禁用。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|10|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-datarefreshmaxhistory-int"></a>-DataRefreshMaxHistory \<int >  
 指定保留数据刷新处理的历史记录的时间长度。 此信息显示在为使用数据刷新的每个工作簿保留的数据刷新历史记录页中。 它还出现在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板中。 默认值为 365 天。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|365|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-healthbasedallocation-switch"></a>-HealthBasedAllocation\<切换 >  
 指定基于运行状况的分配算法，该算法将连接请求转发到其 CPU 和内存资源的可用性最高的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器。 这是默认分配算法。 HealthBasedAllocation 和 RoundRobinBasedAllocation 是互斥的。 只能指定其中的一个。 如果您将它们都设置为 false，将使用 HealthBasedAllocation，因为它是默认值。 如果您将它们都设置为 true，将会收到验证错误。 这些参数的语法包括仅输入参数名称，或者输入 parameter:$true 或 parameter:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-loadstoconnectionsratiocollectioninterval-int"></a>-LoadsToConnectionsRatioCollectionInterval \<int >  
 指定为计算加载与连接之比而对加载和连接事件进行计数的时间间隔（以小时为单位）。 默认情况下，系统会每 4 小时计算一个新比率。 有效值为 1 至 24。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|4|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-loadstoconnectionsratiolimit-int"></a>-LoadsToConnectionsRatioLimit \<int >  
 指定加载事件与连接事件的比率，用作服务器运行状况的一个指标。 默认值为 20%。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|20|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-memorydatabaseholdlimit-int"></a>-MemoryDatabaseHoldLimit \<int >  
 指定非活动数据库保留在内存中以便支持针对这些数据的新请求的小时数。 只要您对活动数据库进行查询，该活动数据库就会始终保留在内存中，但在该数据库不再处于活动状态后，系统会将该数据库在内存中再保留一段时间，以防出现针对这些数据的更多请求。 默认值为 48 小时。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|48|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-queryreportinginterval-int"></a>-QueryReportingInterval \<int >  
 指定在报告前作为使用情况事件收集查询响应统计信息的秒数。 默认值为 300 秒。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|300|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-roundrobinallocation-switch"></a>-RoundRobinAllocation\<切换 >  
 指定循环分配算法，该算法将连接请求转发到下一个 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 服务器，并且在各可用服务器之间平均交替分配请求，而与服务器负荷无关。 HealthBasedAllocation 和 RoundRobinBasedAllocation 是互斥的。 只能指定其中的一个。 如果您将它们都设置为 false，将使用 HealthBasedAllocation，因为它是默认值。 如果您将它们都设置为 true，将会收到验证错误。 这些参数的语法包括仅输入参数名称，或者输入 parameter:$true 或 parameter:$false。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-unattendedaccount-string"></a>-UnattendedAccount\<字符串 >  
 指定 Secure Store Service 应用程序的目标应用程序名称，该应用程序存储一个预定义的帐户以便运行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新作业。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usagedataretentionperiod-int"></a>-UsageDataRetentionPeriod \<int >  
 指定保留使用情况数据和服务器运行状况统计信息的历史记录的天数。 默认值为 365 天。 将此值设置为 0 将无限期保留所有历史记录。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|365|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usageexpectedresponseupperlimit-int"></a>-UsageExpectedResponseUpperLimit \<int >  
 设置定义预期请求-响应交换的上限。 默认值为 3000 毫秒。 出于报告目的，在 1000 到 3000 毫秒之间完成的任何请求都被视为预期响应。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|3000|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usagelongresponseupperlimit-int"></a>-UsageLongResponseUpperLimit \<int >  
 设置定义长时间运行的请求-响应交换的上限。  上限为 10000 毫秒。 超出此上限的任何请求都属于“超出”类别，因此没有上限。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|10000|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usagequickresponseupperlimit-int"></a>-UsageQuickResponseUpperLimit \<int >  
 设置定义快速请求-响应交换的上限。 默认值为 1000 毫秒。 在 500 到 1000 毫秒之间完成的任何请求都被视为出于报告目的的快速响应。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|1000|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usagetrivialresponseupperlimit-int"></a>-UsageTrivialResponseUpperLimit \<int >  
 指定一个响应时间类别，这些响应时间太短以致出于收集目的不会去考虑。 大多数属于此类别的响应是服务器到服务器的通信。 默认情况下，该值为 500 毫秒。 在 0 到 500 毫秒之间完成的任何请求都是一般请求，并且出于报告目的将被忽略。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|500|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-usageupdatedaylimit-int"></a>-UsageUpdateDayLimit \<int >  
 指定触发警告的阈值（天），该警告针对在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 管理面板中刷新由报表使用的数据文件失败的情况。 默认情况下，系统会每天更新使用情况数据。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Management Dashboard.xlsx 文件（这是管理报告的数据源）将按照相同的计划进行刷新。 如果在一定的天数后未更新该 .xlsx 文件，将触发一个运行状况规则，指示该文件过期。 默认值为 5 天。 有效值为 1 到 30。  
  
|||  
|-|-|  
|必需？|false|  
|位置？|所指定位置|  
|默认值|5|  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|无。|  
  
## <a name="example-1"></a>示例 1  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -AllowCustomWindowsCredentials:$false -UnattendedAccount "MyTargetApp"  
```  
  
 此示例禁用自动创建和管理安全存储区服务目标应用程序以便存储任意 Windows 凭据的数据刷新功能。 它还将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 无人参与的数据刷新帐户设置为预定义的目标应用程序。  
  
 使用 Get-powerpivotserviceapplication 可以获取有效的标识。  
  
## <a name="example-2"></a>示例 2  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklm -HealthBasedAllocation  
```  
  
 该示例指定基于运行状况的分配算法，该算法将连接请求转发到其资源的可用性最高的服务器。  
  
 使用 Get-powerpivotserviceapplication 可以获取有效的标识。  
  
## <a name="example-3"></a>示例 3  
  
```  
C:\PS>Set-PowerPivotServiceApplication -identity 1234567-890a-bcde-fghijklmn -BusinessHoursStartTime "07:15AM" -BusinessHoursEndTime "08:00PM"  
```  
  
 该示例说明如何设置工作日的开始和结束小时，它们用作计划 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 数据刷新的计划选项。 计划可以指定工作时间后的选项，以便在下班后运行数据刷新。  
  
 使用 Get-powerpivotserviceapplication 可以获取有效的标识。  
  
  
