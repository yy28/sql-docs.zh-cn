---
title: "SQL Server 2012 SP1 发行说明 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: 49
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 978e780dd19e34c27ceef49ff8388f6ae1f155ed
ms.openlocfilehash: bb97a542834adce9221b55f54c4bf5657586f187
ms.contentlocale: zh-cn
ms.lasthandoff: 09/02/2017

---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
本发行说明文档介绍了在安装 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 或者解决其相关问题之前应该了解的一些已知问题。 本发行说明文档只能在线下载，而不提供有关的安装介质，并且本文档将定期更新。  
  
## <a name="bkmk_top"></a>目录  
[1.0 安装之前](#bmk_Install)  
  
[2.0 Analysis Services 和 PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Change Data Capture Service 和 Designer for Oracle by Attunity](#bkmk_CDC)  
  
[7.0 SQL Server 数据层应用程序框架 (DACFx)](#DACFx)  
  
[8.0 此 Service Pack 中已修复的已知问题](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 安装之前  
在安装 SQL Server 2012 SP1 之前，请考虑以下信息。  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1 如果使用同一 IP 地址，则重新安装 SQL Server 故障转移群集实例失败  
**问题：** 如果在安装 SQL Server 故障转移群集实例期间指定不正确的 IP 地址，安装将失败。 卸载失败的实例后，如果尝试使用同一实例名称和正确的 IP 地址重新安装 SQL Server 故障转移群集实例，安装将失败。 安装失败是由于上次安装留下的重复资源组造成的。  
  
**解决方法：** 要解决此问题，请在重新安装时使用不同的实例名称，或在重新安装前手动删除该资源组。 有关详细信息，请参阅 [在 SQL Server 故障转移群集中添加或删除节点](http://msdn.microsoft.com/library/ms191545)。  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2 正确选择要下载及安装的文件  
请使用下表来确定要下载和安装的文件。 安装 Service Pack 之前请验证您的系统是符合要求的。 表中链接的下载页上提供了系统要求。  
  
|如果您目前已经安装的版本是...|而您需要...|请下载和安装...|  
|-------------------------------------------|----------------------|---------------------------|  
|**32 位安装：**|||  
|SQL Server 2012 的任何版本的 32 位版|升级到 SQL Server 2012 SP1 的 32 位版|SQLServer2012SP1-KB2674319-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|SQL Server 2012 RTM Express 的 32 位版|升级到 SQL Server 2012 Express SP1 的 32 位版|SQLServer2012SP1-KB2674319-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|仅 SQL Server 2012 的客户端和可管理性工具（包括 SQL Server 2012 Management Studio）的 32 位版|将客户端和可管理性工具升级到 SQL Server 2012 SP1 的 32 位版|SQLManagementStudio_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|SQL Server 2012 Management Studio Express 的 32 位版|升级到 SQL Server 2012 SP1 Management Studio Express 的 32 位版|SQLManagementStudio_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|SQL Server 2012 的任何版本的 32 位版 **和** 客户端和可管理性工具（包括 SQL Server 2012 RTM Management Studio）的 32 位版|将所有产品都升级到 SQL Server 2012 SP1 的 32 位版|SQLServer2012SP1-KB2674319-x86-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|[Microsoft SQL Server 2012 RTM 功能包](http://www.microsoft.com/download/details.aspx?id=16978)(#microsoft-sql-server-2012-rtm-功能包) 中一种或多种工具的 32 位版|将工具升级到 Microsoft SQL Server 2012 SP1 功能包的 32 位版|[Microsoft SQL Server 2012 SP1 功能包](http://go.microsoft.com/fwlink/p/?LinkID=268266)中的一个或多个文件|  
|没有安装 SQL Server 2012 的 32 位版|安装包括 SP1 的 32 位 Server 2012（预装了 SP1 的新实例）|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **和** SQLServer2012SP1-FullSlipstream-x86-ENU.box（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|没有安装 SQL Server 2012 Management Studio 的 32 位版|安装 32 位 SQL Server 2012 Management Studio（包括 SP1）|SQLManagementStudio_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=267905)(#此处)）|  
|无 32 位版 SQL Server 2012 RTM Express|安装 32 位 SQL Server 2012 Express（包括 SP1）|SQLEXPR32_x86_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkId=267905)(#此处)）|  
|**SQL Server 2008** 或 **SQL Server 2008 R2**的 32 位安装|**就地升级** 到 32 位 SQL Server 2012（包括 SP1）|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **和** SQLServer2012SP1-FullSlipstream-x86-ENU.box（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|**64 位安装：**|||  
|SQL Server 2012 的任何版本的 64 位版|升级到 SQL Server 2012 SP1 的 64 位版|SQLServer2012SP1-KB2674319-x64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|SQL Server 2012 RTM Express 的 64 位版|升级到 SQL Server 2012 SP1 的 64 位版|SQLServer2012SP1-KB2674319-x64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|仅 SQL Server 2012 的客户端和可管理性工具（包括 SQL Server 2012 R2 Management Studio）的 32 位版|将客户端和可管理性工具升级到 SQL Server 2012 SP1 的 64 位版|SQLManagementStudio_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|SQL Server 2012 Management Studio Express 的 64 位版|升级到 SQL Server 2012 SP1 Management Studio Express 的 64 位版|SQLManagementStudio_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|SQL Server 2012 的任何版本的 64 位版 **和** 客户端和可管理性工具（包括 SQL Server 2012 RTM Management Studio）的 64 位版|将所有产品都升级到 SQL Server 2012 SP1 的 64 位版|SQLServer2012SP1-KB2674319-x64-ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|[Microsoft SQL Server 2012 RTM 功能包](http://www.microsoft.com/download/en/details.aspx?id=16978)(#microsoft-sql-server-2012-rtm-功能包) 中一种或多种工具的 64 位版|将工具升级到 Microsoft SQL Server 2012 SP1 功能包的 64 位版|[Microsoft SQL Server 2012 SP1 功能包](http://go.microsoft.com/fwlink/p/?LinkID=268266)中的一个或多个文件|  
|没有安装 SQL Server 2012 的 64 位版|安装包括 SP1 的 64 位 Server 2012（预装了 SP1 的新实例）|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **和** SQLServer2012SP1-FullSlipstream-x64-ENU.box（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
|没有安装 SQL Server 2012 Management Studio 的 64 位版|安装 64 位 SQL Server 2012 Management Studio（包括 SP1）|SQLManagementStudio_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|无 64 位版 SQL Server 2012 RTM Express|安装 64 位 SQL Server 2012 Express（包括 SP1）|SQLEXPR_x64_ENU.exe（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=267905)(#此处)）|  
|**SQL Server 2008** 或 **SQL Server 2008 R2**的 64 位安装|**就地升级** 到 64 位 SQL Server 2012（包括 SP1）|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **和** SQLServer2012SP1-FullSlipstream-x64-ENU.box（从 [此处](http://go.microsoft.com/fwlink/p/?LinkID=268158)(#此处)）|  
  
![与“返回首页”链接一起使用的箭头图标](../sql-server/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[内容](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services 和 PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1 PowerPivot 配置工具未创建 PowerPivot 库  
**问题：** PowerPivot 配置工具设置工作组网站，因此不创建 PowerPivot 库。  
  
**解决方法：** 创建一个新应用程序（库）。  
  
1.  确认网站集功能 **“针对网站集的 PowerPivot 功能集成”** 处于活动状态。  
  
2.  从现有网站的 **“网站内容”** 页上，单击 **“添加应用程序”**。  
  
3.  单击 **“PowerPivot 库”**。  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2 若要将 PowerPivot for Excel 与 Excel 2013 一起使用，您必须使用与 Excel 一起安装的外接程序  
**问题：** 对于 Office 2010，PowerPivot for Excel 是可从 [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx)(#http://www.microsoft.com/bi/powerpivot.aspx) 下载的独立外接程序。 也可以从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=29074)下载它。 请注意，有两个可供下载的 PowerPivot 外接程序版本：一个是 SQL Server 2008 R2 随附的版本，另一个是 SQL Server 2012 随附的版本。 但对于 Office 2013，PowerPivot for Excel 随 Office 一起提供并且在您安装 Excel 时安装。 尽管 PowerPivot for Excel 2010 的 SQL Server 2008 R2 和 SQL Server 2012 版本与 Excel 2013 不兼容，但是，如果您想要将 Excel 2010 与 Excel 2013 并行运行，仍可以在您的客户端计算机上安装 PowerPivot for Excel 2010。 换言之，Excel 的两个版本可以共存，因此可以使用相应的 PowerPivot 外接程序。  
  
**解决方法：**若要使用 PowerPivot for Excel 2013，则必须启用 COM 外接程序。 从 Excel 2013，选择“**文件**” | “**选项**” | “**外接程序**”。从“**管理**”下拉框中，选择“**COM 外接程序**”，然后单击“**执行**”。 从“ **COM 外接程序**”中，选择 **Microsoft Office PowerPivot for Excel 2013** ，然后单击“ **确定**”。  
  
![与“返回首页”链接一起使用的箭头图标](../sql-server/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[内容](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1 在安装 Reporting Services 前安装和配置 SharePoint Server 2013  
**问题：** 在安装 SQL Server Reporting Services (SSRS) **前** 完成以下操作。  
  
1.  运行 SharePoint 2013 产品准备工具。  
  
2.  安装 SharePoint Server 2013。  
  
3.  运行 SharePoint 2013 产品配置向导或完成等效的配置步骤来配置 SharePoint 场。  
  
**解决方法：**  如果在配置 SharePoint 场前安装了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式，所需的解决方法取决于安装了哪些其他组件。  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2 SharePoint Server 2013 中的 Power View 需要 Microsoft.AnalysisServices.SPClient.dll  
**问题：**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 未安装必需的组件 **Microsoft.AnalysisServices.SPClient.dll**。 如果在 SharePoint 模式下安装 SharePoint Server 2013 Preview 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ，但是未下载和安装 PowerPivot for SharePoint 2013 安装程序包 **spPowerPivot.msi** ，Power View 将不起作用且出现以下症状：  
  
**症状：** 当您尝试创建 Power View 报表时，会看到一条类似于以下内容的错误消息：  
  
-   “无法与数据源建立连接...”  
  
内部错误详细信息将包含如下消息：  
  
-   “连接字符串属性‘用户标识’不支持值‘SharePoint 主体’。”  
  
**解决方法：** 在 SharePoint Server 2013 上安装 PowerPivot for SharePoint 2013 安装程序包 (**spPowerPivot.msi**)。 该安装程序包作为 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能包的一部分提供。 可以从 [!INCLUDE[msCoName](../includes/msconame-md.md)] 下载中心的 [SQL Server 2012 SP1 功能包](http://go.microsoft.com/fwlink/p/?LinkID=268266)(http://go.microsoft.com/fwlink/p/?LinkID=286266) 下载此功能包。  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3 在执行预定的数据刷新后删除 PowerPivot 工作簿中的 Power View 工作表  
**问题**：在 PowerPivot for SharePoint 外接程序中，对包含 Power View 的工作簿使用“ **计划的数据刷新** ”将删除所有 Power View 工作表。  
  
**解决方法**：要将 **Scheduled Data Refresh** 用于 Power View 工作簿，请创建仅作为数据模型的 PowerPivot 工作簿。 使用您的 Excel 工作表和 Power View 工作表创建单独的工作簿，将它链接到包含数据模型的 PowerPivot 工作簿。 应只对包含数据模型的 PowerPivot 工作簿安排执行数据刷新。  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1 DQS 在错误的 SQL Server 2012 版本中提供  
**问题：** 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM 版本中，Data Quality Services (DQS) 功能在 Enterprise、Business Intelligence 和 Developer 版本以外的 SQL Server 版本中提供。 在安装 SQL Server 2012 SP1 后，DQS 将在除 Enterprise、Business Intelligence 和 Developer 版本之外的所有版本中不可用。  
  
**解决方法**：如果您在不支持的版本中使用 DQS，则或者升级到支持的版本，或者从您的应用程序中删除对此功能的依赖关系。  
  
![与“返回首页”链接一起使用的箭头图标](../sql-server/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[内容](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1 在 SQL Server 2012 Express SP1 中提供 SQL Server Management Studio 的完整版本  
SQL Server 2012 Express Service Pack 1 (SP1) 版本包括 SQL Server 2012 Management Studio 的完整版本（以前仅在 SQL Server 2012 DVD 上提供），而非 SQL Server 2012 Management Studio Express。 若要下载和安装 SQL Server 2012 Express SP1，请参阅 [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905)。  
  
![与“返回首页”链接一起使用的箭头图标](../sql-server/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[内容](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Change Data Capture Service 和 Designer for Oracle by Attunity  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1 升级 CDC 服务和设计器  
**问题：** 如果在您安装 SQL Server 2012 SP1 时 Change Data Capture Designer for Oracle 和 Change Data Capture Service for Oracle by Attunity 安装在您的计算机上，则通过安装 SP1 将不会升级这些组件。  
  
**解决方法：** 将 CDC 组件升级到最新版本：  
  
1.  从 [SQL Server 2012 SP1 功能包下载页](http://go.microsoft.com/fwlink/p/?LinkID=268266)下载用于 Change Data Capture Service for Oracle by Attunity 的 .msi 文件。  
  
2.  运行该 .msi 文件。  
  
![与“返回首页”链接一起使用的箭头图标](../sql-server/media/uparrow16x16.gif "与“返回首页”链接一起使用的箭头图标")[内容](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 SQL Server 数据层应用程序框架 (DACFx)  
**就地升级支持**  
  
此版本的数据层应用程序框架 (DACFx) 支持从以前版本就地升级，因此在升级到此版本前，不需要删除以前的 DACFx 安装。 您可以在 [此处](https://msdn.microsoft.com/library/dn702988.aspx)找到 DACFx 的将来版本。  
  
**对选择性 XML 索引的支持**  
  
SQL Server 2012 SP1 包括对 [选择性 XML 索引 (SXI)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44)(#选择性-xml-索引-(sxi)) 这个新 SQL Server 功能的支持，该功能为 XML 列数据提供新的索引编制方式，提高了性能和效率。  
  
DACFx 现在支持所有 DAC 方案和客户端工具中的 SXI 索引。 SXI 仅在最新版本的 SSDT 中受支持。 SSDT RTM 和 2012 年 9 月版本不支持 SXI。  
  
**对本机 BCP 数据格式的支持**  
  
以前，用于存储 DACPAC 和 BACPAC 包中的表数据的数据格式为 JSON。 应用此更新后，本机 BCP 现在为数据永久格式。 这个变化为 DACFx 带来改进的 SQL Server 数据类型精确度，包括对 SQL_Variant 类型的支持以及针对大型数据库的增强数据部署性能。  
  
**创建/部署包时保存 CHECK 约束状态**  
  
以前，DACFx 不在数据库架构中保存对表定义的 CHECK 约束状态 (WITH CHECK/NOCHECK)，也不在 DACPAC 内存储此信息。 当现有表数据违反 CHECK 约束时，此行为可能导致潜在的包部署问题。 应用此更新后，DACFx 现在在从数据库提取时在 DACPAC 内存储 CHECK 约束的当前状态并在包部署时相应还原此状态。  
  
**对 SqlPackage.exe（DACFx 命令行工具）的更新**  
  
-   带数据提取 DACPAC – 从一个活动 SQL Server 或 Windows Azure SQL Database 创建数据库快照文件 (.dacpac)，该文件除了包含数据库架构之外还包含用户表的数据。 可以使用 SqlPackage.exe“发布”操作将这些包发布到新的或现有 SQL Server 或 Windows Azure SQL Database。 包中包含的数据将替代目标数据库中的现有数据。  
  
-   导出 BACPAC - 创建包含数据库架构和用户数据的活动 SQL Server 或 Windows Azure SQL Database 的逻辑备份文件 (.bacpac)，这些架构和数据可用于将数据库从内部 SQL Server 迁移到 Windows Azure SQL Database。 可以在支持的 SQL Server 版本间导出与 Azure 兼容的数据库，之后再导入。  
  
-   导入 BACPAC – 导入 .bacpac 文件以新建或填充空的 SQL Server 或 Windows Azure SQL Database。  
  
MSDN 上的完整 SqlPackage.exe 文档可以在 [此处](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)找到。  
  
**包兼容性**  
  
本版本介绍用于 DAC 包的几个向前兼容方案。  
  
-   本版本创建的不包含 SXI 元素或表数据的 DAC 包可能由以前版本的 DACFx（SQL Server 2012 RTM、SQL Server 2012 CU1 和 DACFx 2012 年 9 月版）使用。  
  
-   以前版本的 DACFx 创建的所有 DAC 包可以由本版本使用。  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 此 Service Pack 中已修复的已知问题  
有关此 Service Pack 中已修复的 Bug 和已知问题的完整列表，请参阅 [此知识库文章](http://support.microsoft.com/kb/2674319)。  
  
[目录](#bkmk_top)  
  
## <a name="see-also"></a>另请参阅  
[如何确定 SQL Server 的版本和版本类别](http://support.microsoft.com/kb/321185)  
[SQL Server 2014 各个版本支持的功能](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  

