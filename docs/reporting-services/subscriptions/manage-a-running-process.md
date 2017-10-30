---
title: "管理正在运行的进程 |Microsoft 文档"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 103472f5003235e0e08c65c40999545ff4d864ee
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="manage-a-running-process"></a>管理运行中的进程
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可监视报表服务器上正在运行的作业的状态。 报表服务器会定期扫描正在进行的作业，并将状态信息写入到报表服务器数据库或针对 SharePoint 模式的服务应用程序数据库中。 如果正在执行以下任意进程，则表明正在处理作业：对远程或本地数据库服务器的查询执行、报表处理以及报表呈现。  
  
 您可以同时管理“用户作业  ”和“系统作业 ”。  
  
-   用户作业是由各个用户或订阅启动的。 这包括按需运行报表，请求报表历史记录快照，手动创建报表快照，以及处理标准订阅等。  
  
-   系统作业是由报表服务器启动的。 系统作业包括计划的报表执行快照、计划的报表历史记录快照以及数据驱动订阅。  
  
 根据报表、查询复杂程度、数据量以及为报表指定的呈现格式，报表处理时间和资源使用情况会有很大的差异。 具有对本地数据源的简单查询的报表通常会在数毫秒内完成，因此从不需要进行管理或优化。 相反，以 PDF 或 Excel 格式呈现的大型报表可能需要很长的处理时间，这取决于硬件资源、传递选项以及是否有其他进程正在并发运行。 在报表服务器上，大多数长时间运行的进程都是一些报表呈现操作以及等待查询处理结束的进程。 有时，您可能希望将计算机脱机，或停止需很长时间才能完成的运行中作业，在这种情况下，则需要取消报表进程。  
  
 可以取消以下进程：  
  
-   按需报表处理。  
  
-   计划报表处理。  
  
-   各用户拥有的标准订阅。  
  
 取消作业时，取消的仅仅是运行在报表服务器上的进程。 由于报表服务器不管理其他计算机上发生的数据处理，因此必须手动取消其他系统上后来孤立的查询进程。 可以考虑指定查询超时值以自动关闭执行时间过长的查询。 有关详细信息，请参阅[获得报表和共享数据集处理 &#40; 设置超时值SSRS &#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). 有关临时暂停报表的详细信息，请参阅 [禁用或暂停报表和订阅处理](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)。  
  
> [!NOTE]  
>  在极少数情况下，可能需要重新启动服务器才能取消进程。 对于 SharePoint 模式，您可能需要重新启动承载 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的应用程序池。 有关详细信息，请参阅 [启动和停止报表服务器服务](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)。  
  
 本主题内容：  
  
-   [查看和取消作业（本机模式）](#bkmk_native)  
  
-   [查看和取消作业（SharePoint 模式）](#bkmk_sharepoint)  
  
-   [以编程方式管理作业](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> 查看和取消作业（本机模式）  
 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 查看或取消报表服务器上正在运行的作业。 您必须刷新页面，才能检索当前正在运行的作业的列表或从报表服务器数据库中获取最新的作业状态信息。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到报表服务器之后，您可以打开作业文件夹以查看该报表服务器计算机上当前正在处理的报表的列表。 在“作业属性”页上显示了每个作业的状态信息。 打开“取消报表服务器作业”对话框可以查看所有作业的状态信息。  
  
 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 查看或取消报表服务器上正在运行的作业。 您必须刷新页面，才能检索当前正在运行的作业的列表或从报表服务器数据库中获取最新的作业状态信息。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到报表服务器之后，您可以打开作业文件夹以查看该报表服务器计算机上当前正在处理的报表的列表。 在“作业属性”页上显示了每个作业的状态信息。 打开“取消报表服务器作业”对话框可以查看所有作业的状态信息。  
  
 无法使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 列出或取消模型生成、模型处理或数据驱动订阅。 Reporting Services 没有提供取消模型生成或处理的方法。 但是，您可以按照本主题中的说明取消数据驱动订阅。  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>如何取消报表处理或订阅  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，连接到报表服务器。 有关说明，请参阅 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
2.  打开 **“作业”** 文件夹。  
  
3.  右键单击报表，然后单击**取消作业**。  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>如何取消数据驱动订阅  
  
1.  在文本编辑器中打开 RSReportServer.config 文件。  
  
2.  查找 **IsNotificationService**。  
  
3.  将其设置为 **False**。  
  
4.  保存该文件。  
  
5.  在报表管理器中，从订阅选项卡的报表或从删除数据驱动订阅**我的订阅**。  
  
6.  删除订阅之后，在 RSReportServer.config 文件中查找 **IsNotificationService** ，并将其设置为 **True**。  
  
7.  保存该文件。  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>配置检索作业状态的频率设置  
 正在运行的作业存储在报表服务器的临时数据库中。 您可以修改 RSReportServer.config 文件中的配置设置，以控制报表服务器扫描正在进行的作业的频率，以及正在运行的作业的状态在多长时间间隔后从“新”更改为“正在运行”。 **RunningRequestsDbCycle** 设置指定报表服务器扫描正在运行的进程的频率。 默认情况下，每隔 60 秒记录一次状态信息。 **RunningRequestsAge** 设置指定作业的状态从“新”更改为“正在运行”的时间间隔。  
  
##  <a name="bkmk_sharepoint"></a> 查看和取消作业（SharePoint 模式）  
 使用 SharePoint 管理中心为每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序完成 SharePoint 模式部署中作业的管理。  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>在 SharePoint 模式下管理作业  
  
1.  在 SharePoint 管理中心中，单击 **“管理服务应用程序”**。  
  
2.  查找并单击您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的名称，以打开“管理应用程序”页。  
  
3.  单击 **“管理作业”**。  
  
4.  单击 **“作业 ID”** 查看作业的详细信息。  
  
5.  或单击您的作业的框，然后单击 **“删除”** 以取消作业。 删除作业并不会删除订阅。  
  
##  <a name="bkmk_programmatically"></a> 以编程方式管理作业  
 您可以通过编程方式或使用脚本来管理作业。 有关详细信息，请参阅 <xref:ReportService2010.ReportingService2010.ListJobs%2A>、 <xref:ReportService2010.ReportingService2010.CancelJob%2A>。  
  
## <a name="see-also"></a>另请参阅  
 [取消报表服务器作业 (Management Studio)](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [作业属性 &#40;Management Studio &#41;](../../reporting-services/tools/job-properties-management-studio.md)   
 [修改 Reporting Services 配置文件 &#40;RSreportserver.config &#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [报表管理器 &#40;SSRS 本机模式 &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [监视报表服务器性能](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
  

