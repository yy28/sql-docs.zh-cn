---
title: 服务器属性“高级”页 - Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 11/05/2019
ms.openlocfilehash: defadad0d3a2545ba3d794d5d9c38c5734d3e9af
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73638029"
---
# <a name="server-properties-advanced-page---reporting-services"></a>服务器属性“高级”页 - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

使用此页可以针对报表服务器设置系统属性。 可通过多种方法来设置系统属性。 此工具提供了一个图形用户界面，您不必编写代码即可设置属性。

若要打开此页，请启动 SQL Server Management Studio，连接到报表服务器实例，右键单击报表服务器名称，然后选择“属性”  。 选择“高级”  打开此页。

## <a name="options"></a>选项

**EnableMyReports**  
指示是否启用“我的报表”功能。 值为 **true** 表示已启用该功能。  

**MyReportsRole**  
对用户的“我的报表”文件夹创建安全策略时所用角色的名称。 默认值是 **My Reports Role**秒。  

**EnableClientPrinting**  
确定是否可从报表服务器下载 RSClientPrint ActiveX 控件。 有效值为 **true** 和 **false**。 默认值为 **true**。 有关此控件所需的其他设置的详细信息，请参阅 [启用和禁用 Reporting Services 的客户端打印](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  

**EnableExecutionLogging**  
指示报表执行日志记录是否处于启用状态。 默认值为 **true**。 有关报表服务器执行日志的详细信息，请参阅 [报表服务器 ExecutionLog 和 ExecutionLog3 视图](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  

**ExecutionLogDaysKept**  
在执行日志中保留报表执行信息的天数。 此属性的有效值包括 **-1** 到 **2**、**147**、**483**、**647**。 如果值为“-1”，则不会从执行日志表中删除条目  。 默认值是 **60**秒。  

> [!NOTE]
> 将值设置为“0”会从执行日志中删除所有条目   。 值为“-1”将保留执行日志的条目，不会删除它们  。

**RDLXReportTimetout** 在报表服务器命名空间中托管的所有报表的 RDLX 报表（SharePoint Server 中的 Power View 报表）处理超时值（以秒为单位）  。 该值可在报表级别进行重写。 如果设置了此属性，则超过指定时间后报表服务器会尝试停止处理报表。 有效值为 **-1** 到 **2**,**147**,**483**,**647**。 如果值为 **-1**，则处理期间命名空间中的报表不会超时。 默认值是 **1800**秒。

**SessionTimeout** 会话保持活动状态的时间长度（以秒为单位）。 默认值是 **600**秒。  

**SharePointIntegratedMode**  
此只读属性指示服务器模式。 如果此值为 False，则报表服务器在本机模式下运行。  

**SiteName**  
在 Web 门户的页面标题中显示的报表服务器站点的名称。 默认值是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]秒。 此属性可以是空字符串。 最大长度为 8,000 个字符。  

**StoredParametersLifetime** 指定所存储的参数能够保存的最大天数。 有效值为 **-1**、 **+1** 到 **2,147,483,647**。 默认值为 **180** 天。  

**StoredParametersThreshold**  
指定报表服务器可以存储的参数值的最大数目。 有效值为 **-1**、 **+1** 到 **2,147,483,647**。 默认值是 **1500**秒。  

**UseSessionCookies**  
指示报表服务器与客户端浏览器通信时是否应使用会话 cookie。 默认值为 **true**。  

**ExternalImagesTimeout**  
确定在连接超时之前，必须对外部映像文件检索的时间长度。默认值为 **600** 秒。  

**SnapshotCompression** 此时刻报表服务器的快照。

**SnapshotCompression**  
定义如何压缩快照。 默认值是 **SQL**秒。 有效值如下：

|值|描述|
|---------|---------|
|**SQL**|在存储到报表服务器数据库中时压缩快照。 此压缩操作是当前的行为。|
|**无**|不压缩快照。|
|**全部**|针对所有的存储选项（包括报表服务器数据库或文件系统）压缩快照。|

**SystemReportTimeout**  
在报表服务器命名空间中托管的所有报表的默认报表处理超时值（以秒为单位）。 该值可在报表级别进行重写。 如果设置了此属性，则超过指定时间后报表服务器会尝试停止处理报表。 有效值为 **-1** 到 **2**,**147**,**483**,**647**。 如果值为 **-1**，则处理期间命名空间中的报表不会超时。 默认值是 **1800**秒。  

**SystemSnapshotLimit**  
为报表存储的快照的最大数目。 有效值为 **-1** 到 **2**,**147**,**483**,**647**。 如果值为 **-1**，则无快照限制。  

**AccessControlAllowCredentials**  
指示当“凭据”标记设置为 true 时，是否可以公开对客户端请求的响应。 默认值是 **false**秒。

**AccessControlAllowHeaders** 客户端发出请求时，服务器允许的以逗号分隔的标头列表。 此属性可为空字符串，指定 * 可允许所有标头。

**AccessControlAllowMethods** 当客户端发出请求时，服务器允许的以逗号分隔的 HTTP 方法列表。 默认值为（GET、PUT、POST、PATCH、DELETE），指定 * 可允许所有方法。

**AccessControlAllowOrigin** 当客户端发出请求时，服务器允许的以逗号分隔的来源列表。 默认值为空白，这将阻止所有请求，指定 * 可在未设置凭据时允许所有源，如果指定凭据，则必须指定源的显式列表。

**AccessControlExposeHeaders** 服务器将向客户端公开的以逗号分隔的标头列表。 默认值为空。

**AccessControlMaxAge** 指定预备请求结果可缓存的秒数。 默认值为 600（10 分钟）。

**AllowedResourceExtensionsForUpload**（仅限 Power BI 报表服务器和 Reporting Services 2017 及更高版本）可上传到报表服务器的资源的扩展集。 不需要包含的内置文件类型的扩展名，如 &ast;.rdl 和 &ast;.pbix。 默认扩展名为“&ast;、&ast;.xml、&ast;.xsd、&ast;.xsl、&ast;.png、&ast;.gif、&ast;.jpg、&ast;.tif、&ast;.jpeg、&ast;.tiff、&ast;.bmp、&ast;.pdf、&ast;.svg、&ast;.rtf、&ast;.txt、&ast;.doc、&ast;.docx、&ast;.pps、&ast;.ppt、&ast;.pptx”。

**RestrictedResourceMimeTypeForUpload**不允许用户使用上传内容的 mime 类型集。 已存储为受限 mime 类型的任何资源只能作为应用程序/八进制流下载，而不能由浏览器打开/执行。  默认情况下，此列表中不包含受限制的项，但建议组织填充此项以提供最安全的体验。

**EditSessionCacheLimit**  
指定可在一个报表编辑会话中处于活动状态的数据缓存条目数。 默认数量为 5。  

**EditSessionTimeout**  
指定报表编辑会话超时之前的秒数。默认值为 7200 秒（两小时）。  

**EnableIntegratedSecurity**  
确定报表数据源连接是否支持 Windows 集成安全性。 默认值为 **True**。 有效值如下：

|值|描述|
|---------|---------|
|**True**|已启用 Windows 集成安全性。|
|**False**|未启用 Windows 集成安全性。 配置为使用 Windows 集成安全性的报表数据源不会运行。|

**EnableLoadReportDefinition**  
选中此选项可以指定用户是否可以从报表生成器报表中执行计划外报告执行。 设置此选项即可确定报表服务器的 **EnableLoadReportDefinition** 属性值。  

如果清除此选项，则该属性设置为 False。 报表服务器将不会为使用报表模型作为数据源的报表生成“点击链接型报表”。 将阻止对 LoadReportDefinition 方法的任何调用。  

如果关闭此选项，则会缓解恶意用户通过用 LoadReportDefinition 请求使报表服务器重载来启动拒绝服务攻击的威胁。  

**EnableRemoteErrors**  
包括外部错误信息（例如，有关报表数据源的错误信息），其中包含针对从远程计算机请求报表的用户返回的错误消息。 有效值为 **true** 和 **false**。 默认值是 **false**秒。 有关详细信息，请参阅[启用远程错误 (Reporting Services)](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)。  

**EnableCustomVisuals**（仅适用于 Power BI 报表服务器） 启用 Power BI 自定义视觉对象的显示。 值为 True/False。 默认值为 True  。  

**ExecutionLogLevel** 设置执行日志级别。 默认为正常  。

**InterProcessTimeoutMinutes** 设置进程超时（以分钟为单位）。 默认值为 30  。

**MaxFileSizeMb** 设置报表的最大文件大小（以 MB 为单位）。 默认值为 1000 *。最大值为 2000*。

**ModelCleanupCycleminutes** 设置模型清理周期（以分钟为单位）。 默认为 15  .

**OfficeAccessTokenExpirationSeconds**（仅适用于 Power BI 报表服务器） 设置希望 Office 访问令牌到期的时间（以秒为单位）。 默认值为 60  。

**OfficeOnlineDiscoveryURL**（仅适用于 Power BI 报表服务器） 设置用于查看 Excel 工作簿的 Office Online Server 实例地址。

**RequireIntune**：需要 Intune 才能通过 Power BI 移动应用访问组织的报表。 默认值为 False  。

**ScheduleRefreshTimeoutMinutes**（仅限 Power BI 报表服务器）：设置所需的计划刷新超时时间。默认值为 120  。

**ShowDownloadMenu**：启用客户端工具下载菜单。 默认值为 true  。

**SupportedHyperlinkSchemes** ***（仅限 Power BI 报表服务器）*** 设置允许在可呈现的“超链接”操作上定义的 URI 方案的逗号分隔列表，或设置“&ast;”以启用所有超链接方案。 例如，设置“http、https”将允许指向“https://www. contoso.com”的超链接，但将删除指向“mailto:bill@contoso.com”或“javascript:window.open(‘www.contoso.com’, ‘_blank’)”的超链接。 默认为“&ast;”。

**TimeInitialDelaySeconds** 设置希望初始时间延迟的时长（以秒为单位）。 默认值为 60  。

**TrustedFileFormat**：设置在浏览器中的 Reporting Services 门户网站下打开的所有外部文件格式。 对于未列出的外部文件格式，浏览器会提示下载选项。 默认值为 jpg、jpeg、jpe、wav、bmp、pdf、img、gif、json、mp4、web 和 png。

**EnablePowerBIReportExportData** ***（仅适用于 Power BI 报表服务器）***  
启用从 Power BI 视觉对象导出 Power BI 报表服务器数据。 值为 True 和 False。  默认值为 True。  

**ScheduleRefreshTimeoutMinutes** ***（仅适用于 Power BI 报表服务器）***  
针对嵌入了 AS 模型的 Power BI 报表的计划刷新的数据刷新超时时间（以分钟为单位）。 默认值为 120 分钟。

**EnableTestConnectionDetailedErrors**  
指示当用户使用报表服务器测试数据源连接时，是否向客户端计算机发送详细的错误消息。 默认值为 **true**。 如果此选项设置为 **false**，则只发送一般错误消息。

## <a name="see-also"></a>另请参阅

[设置报表服务器属性 (Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 属性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[报表服务器系统属性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[为部署和管理任务编写脚本](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[启用和禁用“我的报表”](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
