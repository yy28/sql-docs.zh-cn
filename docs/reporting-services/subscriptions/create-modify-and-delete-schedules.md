---
title: "创建、 修改和删除计划 |Microsoft 文档"
ms.custom: 
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 66a306d07b8556fe43659d4b078e2d31f3d51900
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="create-modify-and-delete-schedules"></a>创建、修改和删除计划
  通过本主题，可以了解有关创建、修改和删除 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 共享计划的信息。  若要在本机模式下管理共享计划，请使用 Web 门户中的“计划”页或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的“共享计划”文件夹。 对于 SharePoint 模式，请使用针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的管理页。  
  
 使用以下方法之一来确定是否正在使用共享计划：  
  
-   **Web 门户：** 在“站点设置”页的“共享计划”页上，查看“上次运行时间”日期、“下次运行时间”日期和“状态”字段中的值。 如果某个计划由于过期而不再运行，其“状态”字段中将会显示过期日期。 有关详细信息，请参阅 [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md)。
  
-   **[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]：** 查看给定共享计划的“报表”页。 此页列出了使用该共享计划的所有报表和共享数据集。 有关详细信息，请参阅 [SQL Server Management Studio 中的 Reporting Services ](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)。
  
-  **日志：** 查看报表执行日志文件或跟踪日志来确定报表是否已按照计划指定的时间运行。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="when-you-delete-a-shared-schedule"></a>删除共享计划时  
必须使用 Web 门户中的“计划”页或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的“共享计划”文件夹来手动删除共享计划。 如果您删除使用中的共享计划，则报表特定计划将替换对该计划的所有引用。  
 
如果删除由多个报表和订阅使用的共享计划，报表服务器将为以前使用该共享计划的每个报表和订阅都创建一个计划。 每个新计划都将包含已在共享计划中指定的日期、时间和重复执行模式。 请注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不提供对于各个计划的集中管理。 如果删除共享计划，则需要为各项单独维护计划信息。  
  
**注意：**  如果不确定是否用过共享计划，请考虑在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] （而不是 Web 门户）中删除共享计划。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 提供的共享计划管理功能与报表管理器相同，不过它还提供了可以显示使用该计划的各个报表名称的“报表”页。  
   
 删除计划和使计划过期是有区别的。 过期日期用于停止计划，但不会删除计划。 因为计划用于自动执行许多功能，所以从不会自动进行删除。 通过过期计划，报表服务器管理员可以查明某个自动执行的过程突然停止的原因。 如果没有过期计划，报表服务器管理员可能会错误地诊断问题，或花费不必要的时间，对运行完全正常的过程进行故障排除。  
 
 ## <a name="when-you-delete-a-report-specific--schedule"></a>删除报表特定计划时  
删除报表或订阅时或者选择不同的报表或订阅运行方式时，将删除报表特定计划和订阅特定计划。 例如，选择“始终用最新数据运行此报表”将删除所创建的将报表作为报表执行快照运行的报表特定计划。  

过期的报表特定计划仍会附加到报表。 您可以通过检查计划的结束日期来确定计划是否已过期。 过期的共享计划仍会保留在“共享计划”列表中。 “状态”字段指示计划是否已过期。 您可以通过延长结束日期来恢复计划，也可以在不再需要计划时删除计划引用。  
  
## <a name="bkmk_native"></a> 创建、删除或修改共享计划（Web 门户）  
 创建和修改计划包括设置确定计划运行时间的频率选项。  
  
 您可以在任何时候创建或修改计划。 但是，如果计划在您完成修改之前已经开始运行，则使用计划的修改前版本。 修改的计划必须在保存后才能生效。  
  
 如果您正在修改某个共享计划，可以在进行更改前将其暂停。 当您恢复该计划时，更改立即生效。  

1.  在 Web 门户中，在工具栏中单击“设置”![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png)。 **注意：** 如果“站点设置”不可用，则说明你没有访问站点设置的权限。
2.  单击“站点设置”。  
3.  单击 **“计划”**。  
4.  单击 **“新建计划”**。 若要修改现有计划，请单击计划的名称。  
5.  为计划键入说明性名称。  
6.  选择 **“时”**、 **“天”**、 **“周”**或 **“月”**。 单击 **“一次”** 可以创建仅运行一次的计划。 指定计划的上述基本设置之后，页面上将会显示其他选项。  
7.  根据需要，可以选择开始计划的日期。 默认值为当天。 选择以后的某一天可以推迟计划的开始时间。  
8.  根据需要，可以选择结束计划的日期。 计划将在此日期停止运行，但不会删除。  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="to-delete-a-shared-schedule-web-portal"></a>删除共享计划（Web 门户）  
  
1.  在 Web 门户中，单击全局工具栏上的“站点设置”。     
2.  在该页的 **“其他”** 部分中，单击 **“管理共享计划”**。  
3.  选中要删除的计划旁边的复选框，再单击 **“删除”**。  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>创建、删除或修改共享计划 (Management Studio)  
 共享计划包含的计划和重复执行信息可供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器上运行的任意数量的已发布报表和订阅使用。 如果有多个同时运行的报表和订阅，则可为这些作业创建共享计划。 如果随后想要更改重复执行模式或结束日期，可以在一个位置进行更改。  
  
 共享计划易于维护，并且在管理计划操作方面为您提供了更多的灵活性。 例如，您可以暂停和恢复共享计划。 此外，如果您发现同时运行的计划操作过多，还可以创建多个在不同时间运行的共享计划，然后调整计划信息直到整个报表服务器上的处理负荷分布均匀。  
  
### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>创建或修改共享计划 (Management Studio)  
  
1.  启动 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 并连接到报表服务器实例。  
2.  在对象资源管理器中，展开报表服务器节点。  
3.  右键单击“共享计划”文件夹，再单击“新建计划”。 将显示 **“新建共享计划”** 对话框的“常规”页。  
  
     若要修改现有的共享计划，请展开“共享计划”文件夹，右键单击要修改的计划，再单击“属性”。  
  
4.  为计划键入说明性名称。  
5.  根据需要，可以选择开始计划的日期。 默认值为当天。  
6.  根据需要，可以选择结束计划的日期。 计划将在此日期停止运行，但不会删除。  
7.  若要配置重复执行的计划，请选择 **“小时”**、 **“天”**、 **“周”**或 **“月”**。 此时，将显示其他选项。 使用这些附加选项可以根据前面选择的小时、天、周或月来配置计划频率。  
  
     或者，若要指定一次性（不重复执行）计划，请选择“一次”，然后指定“开始时间”。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>删除共享计划 (Management Studio)  
  
1.  在对象资源管理器中，展开报表服务器节点。  
2.  要验证共享计划当前未由报表使用，请展开“共享计划”文件夹，右键单击计划，然后单击“属性”。
3. 单击“报表”选项卡以查看当前使用计划的报表的列表。
单击“取消”
4.  展开“共享计划”文件夹，右键单击要删除的计划，再单击“删除”。 将显示 **“删除目录项”** 对话框。  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 如果删除由多个报表和订阅使用的共享计划，报表服务器将为以前使用该共享计划的每个报表和订阅都创建一个计划。 每个新计划都将包含已在共享计划中指定的日期、时间和重复执行模式。
 
##  <a name="bkmk_sharepoint"></a> 创建和管理共享计划（SharePoint 模式）  
 若要在 SharePoint 站点上创建、修改或删除共享计划，您必须为站点管理员。  
  
 您可以用描述性名称标识特定计划。 如果未指定名称，将根据有关计划的事实数据（例如计划的重复执行模式或其运行日期和时间）创建一个默认名称。  
  
> [!NOTE]  
>  创建共享计划需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。  
  
### <a name="create-shared-schedules-sharepoint-mode"></a>创建共享计划（SharePoint 模式）  
1.  单击 **“网站操作”**。  
2.  单击 **“网站设置”**。  
3.  在 Reporting Services 部分中，单击 **“管理共享计划”**。  
4.  单击 **“添加计划”** 以打开“计划属性”页。  
5.  为计划输入描述性名称。 在用来处理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表的应用程序页中，此名称将显示在整个站点的计划定义页的下拉列表中。 避免使用冗长难读的名称。 请遵循将大多数说明信息放在名称开头的命名约定。  
6.  选择频率。 根据选择的频率，该页中显示的计划选项可能会发生更改以支持该频率（例如，如果选择“月”，该页中将显示每个月的名称）。  
7.  定义计划。 在一个计划中无法支持所有形式的计划组合。  
8.  设置开始和结束日期。  
9. 单击 **“确定”**。  
  
### <a name="delete-shared-schedules-sharepoint-mode"></a>删除共享计划（SharePoint 模式）  
 所有计划都必须以手动方式删除，无论是共享计划还是报表特定计划。 如果删除某个正在使用中的共享计划，则对该计划的所有引用将替换为未指定的自定义计划（也就是说，不包含日期或时间信息的自定义计划）。  
  
1.  单击 **“网站操作”**。  
2.  单击 **“网站设置”**。  
3.  在 Reporting Services 部分中，单击 **“管理共享计划”**。  
4.  选择计划，并单击 **“删除”**。  
 
  
## <a name="see-also"></a>另请参阅  
 [Schedules](../../reporting-services/subscriptions/schedules.md)   
 [暂停和恢复共享计划](../../reporting-services/subscriptions/pause-and-resume-shared-schedules.md)   
 [缓存报表（报表管理器）](../../reporting-services/report-server/cache-a-report-report-manager.md)   
 [向报表历史记录添加快照（报表管理器）](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  

