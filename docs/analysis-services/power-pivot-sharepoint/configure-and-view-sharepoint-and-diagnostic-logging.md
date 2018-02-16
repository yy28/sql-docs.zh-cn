---
title: "配置和查看 SharePoint 和诊断日志记录 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 85f62d29-cdc6-45b3-be1f-ff1182939858
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: ed3dbf6b45af894f4f2f841d7c8b3496a332028f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="configure-and-view-sharepoint-and-diagnostic-logging"></a>配置和查看 SharePoint 和诊断日志记录
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器操作、事件和消息均记录在 SharePoint 日志文件中。 使用此主题中的信息可配置日志记录级别和查看日志文件信息。 您可以控制要将哪些 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器事件记录到文件中。 还可以控制所记录的消息的严重性。 有关详细信息，请参阅 [配置使用情况数据收集 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)。  
  
 本主题内容：  
  
-   [日志文件位置](#bkmk_filelocation)  
  
-   [修改单独事件类别的诊断日志记录级别](#bkmk_modifyloglevels)  
  
-   [如何查看 SharePoint 日志文件](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> 日志文件位置  
 默认情况下，SharePoint 日志文件保存到以下位置：  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 LOGS 文件夹包含日志文件 (`.log`)、数据文件 (`.txt`) 和使用情况文件 (`.usage`)。 SharePoint 跟踪日志的文件命名约定是服务器名称后跟日期和时间戳。 SharePoint 跟踪日志会定期创建并在每次运行 IISRESET 时创建。 24 小时的时段中有多个跟踪日志是常见现象。  
  
##  <a name="bkmk_modifyloglevels"></a> 修改单独事件类别的诊断日志记录级别  
 默认情况下， [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 事件的 ULS 日志记录设置为“中” 。 此设置是 SQL Server 2012 中新增的设置。 如果您是从先前版本升级的服务器，日志记录级别可能仍设置为“详细” ，这是 SQL Server 2008 R2 中的默认级别。 如果你习惯于查看 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器使用率信息的 ULS 日志，则会发现在实施此更改后， [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器操作的相关信息变少了。  
  
 除了异常（类型为“高” ）之外，其他所有 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 消息均归入“详细”类别。 如果要将日常服务器操作（如连接、请求或查询报告）等条目记入日志，则必须将日志记录级别设置为“详细”。  
  
 修改各个事件类别的诊断日志记录级别：  
  
1.  在 SharePoint 管理中心中，单击 **“监视”**。  
  
2.  单击 **“配置诊断日志记录”**。  
  
3.  滚动到“[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务”。  
  
4.  展开类别，然后选择单独类别。  
  
     “应用程序页面请求” 指定了在定位 [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] 以便加载 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 数据源以及与场中的其他服务器通信时，由服务应用程序触发的事件。  
  
     “请求处理” 指定了查询请求针对场中服务器上加载的 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 数据库触发的事件。  
  
     “使用率” 指定了与 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 使用率数据收集相关的事件。  
  
5.  在“要报告给事件日志的严重程度最低的事件”中，选择 **“无”** 将禁用该类别的事件日志记录，选择 **“错误”** 将只记录错误事件。  
  
6.  选择 **“详细”** ，可将所有事件记录到事件日志中。  
  
7.  在“要报告给跟踪日志的严重程度最低的事件”中，选择 **“无”** 将禁用该类别的跟踪，选择 **“错误”** 将只跟踪错误。  
  
8.  选择 **“详细”** ，可将所有事件记录到跟踪日志中。  
  
9. 单击 **“确定”**。  
  
##  <a name="bkmk_how2viewlogfiles"></a> 如何查看 SharePoint 日志文件  
 日志文件是文本文件。 可以在任何文本编辑器中打开它们。 还可以使用第三方日志查看器应用程序。  
  
#### <a name="use-a-text-editor"></a>使用文本编辑器  
 如果使用文本编辑器排除 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器错误，下列提示可帮助您在文件中定位相关信息：  
  
-   对于与发布、查看或刷新 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 工作簿相关的错误，在日志文件中搜索工作簿的名称。  
  
-   对于提供了相关 ID 的错误，复制 ID 并将其用作在日志文件中搜索时的搜索项。  
  
-   搜索错误状态“高”或“异常”。 搜索“[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务”。  
  
-   如果知道发生错误的时间，使用日期和时间信息来缩小必须搜索的条目范围。  
  
#### <a name="use-a-log-viewer-application"></a>使用日志查看器应用程序  
 尽管可以使用文本编辑器来逐个查看跟踪日志，但是允许您将多个日志文件一起查看的日志查看器应用程序会有用得多。 幸运的是，Codeplex 网站上有多个第三方日志查看器应用程序可供下载，这些应用程序可帮助您在单个工作区中查看多个跟踪日志。  
  
 下面的说明包含指向您可以从 Codeplex 下载的常用 SharePoint ULS 日志查看器的链接。  
  
1.  转到 Codeplex 站点上的 [SharePoint 日志查看器](http://sharepointlogviewer.codeplex.com) 或 [SharePoint ULS 日志查看器](http://go.microsoft.com/fwlink/?LinkId=150052) 。  
  
2.  单击 **“Downloads”** （下载）选项卡。  
  
3.  单击可执行文件。 该可执行文件是 **SharePointLogViewer.exe** 或 **ULS Viewer 2.0 Binary**。  
  
4.  阅读并接受许可条款。  
  
5.  单击 **“保存”** 以将该软件保存到您的本地系统上。  
  
     如果您正在下载 SharePoint ULS 日志查看器，则将 ULSViewer.zip 保存到下载文件夹。  
  
6.  在 Downloads 文件夹中，右键单击 ULSViewer.zip 并选择 **“全部提取”**。  
  
7.  指定目标文件夹，然后单击 **“提取”**。  
  
8.  在包含所提取的程序文件的文件夹中，双击 **ULSViewer** 并运行该应用程序。  
  
9. 单击位于应用程序窗口左上角的文件夹图标。  
  
10. 浏览到 \Program files\Common Files\Microsoft Shared\Web Server Extensions\14\Logs。  
  
11. 选择一个或多个跟踪日志。 默认情况下，跟踪日志文件名由计算机名加上日期和时间信息组成。 文件类型为“文本文档”。  
  
12. 单击 **“打开”** 并等待文件加载。  
  
13. 使用内置筛选器，基于严重性、进程、类别或用户定义的文本文件来选择记录。 还可以单击列标题更改排序顺序。  
  
#### <a name="entries-for-power-pivot-services"></a>PowerPivot 服务的条目  
 下表描述了 SharePoint 日志文件中最可能存在的针对 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务器操作的条目。  
  
|处理|区域|类别|Level|消息|详细信息|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务|用法|Verbose|不存在当前请求统计信息，无信息可供记录。|按照预定义的间隔，服务将查询响应统计信息作为使用情况事件向使用情况数据收集系统报告。 此消息指示没有查询统计信息可供报告。|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务|Web 前端|Verbose|找到数据源的应用程序服务器开始 =\<*路径*>|收到连接请求时， [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务确定可用的 [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] 以处理该请求。 如果场中只有一个服务器，则在所有情况下都是本地服务器接受请求。|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务|Web 前端|Verbose|定位应用程序服务器成功。|请求已分配到 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务应用程序。|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务|Web 前端|Verbose|重定向请求\< *PowerPivotdata 源*> 到[!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)]。|请求已转发给 [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)]。|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 服务|请求处理|Verbose|重定向请求用户名\<*SharePoint 用户*> 到数据库|已代表 SharePoint 用户创建了与 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] 数据源的模拟连接。|  
  
## <a name="see-also"></a>另请参阅  
 [Power Pivot 使用情况数据收集](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)   
 [查看和阅读 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [配置使用情况数据收集 (PowerPivot for SharePoint)](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
