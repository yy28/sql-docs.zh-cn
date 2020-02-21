---
title: 预加载缓存 (SSRS)| Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b2be1e020354f47aa21dc83f17ff6169bcf2d72
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "66175002"
---
# <a name="preload-the-cache"></a>预加载缓存  
  您可以通过为共享数据集创建缓存刷新计划，为共享数据集预加载缓存。  
  
 您可以通过以下两种方式为报表预加载缓存：  
  
1.  为报表创建缓存刷新计划。 这是首选方法。  
  
2.  使用数据驱动订阅可以用参数化报表的实例预加载缓存。 这也是在早于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]版本中预加载缓存的唯一方法。 有关详细信息，请参阅 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)版本中预加载缓存的唯一方法。  
  
 必须首先满足以下条件才能缓存报表或共享数据集：  
  
-   共享数据集或报表必须已启用缓存。  
  
-   共享数据集或报表的共享数据源必须配置为使用存储凭据或没有凭据。  
  
-   必须运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。  
  
## <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>通过创建缓存刷新计划预加载缓存  
  
1. 启动[报表服务器的 Web 门户](../../reporting-services/web-portal-ssrs-native-mode.md "报表服务器的 Web 门户")。  
  
2. 从主屏幕选择“浏览”，然后通过导航文件夹层次结构找到想要缓存的项目。   
  
3. 从项目的右上角选择省略号，然后从下拉菜单选择“管理”。   
  
4. 从左侧的垂直菜单选择“缓存”选项卡。   
  
5. 选择“缓存此数据集的副本，并在可用时使用它们”单选按钮，以激活数据集缓存。  然后它的下方将出现“缓存过期”部分。  选择以下单选按钮之一：

    - **在 x 分钟后缓存过期**（请输入所需的分钟数来作为 x）。
    - **缓存在计划时间过期**。  Reporting Services 提供共享计划和报表特定计划，来帮助你控制处理、一致性内容和报表分发性能。 有关详细信息，请参阅 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md "Create, Modify, and Delete Schedules")。 对于此缓存过期有多个创建计划选项可选：请选择下面两种计划选项之一：  
      - 选择“共享计划”单选按钮，然后从“选择共享计划”下拉文本框选择计划。   有关更多信息，请参见 [Schedules](../../reporting-services/subscriptions/schedules.md "计划")。  
      - 选择“报表特定计划”单选按钮，如有必要，可以继续选择“编辑计划”链接，来查看“计划详细信息”页。    。  

         ![数据集的 Web 门户缓存过期计划详细信息页](../../reporting-services/report-server/media/preload-the-cache/web-portal-dataset-cache-schedule-details.png "数据集缓存计划详细信息页")

          可从此页选择下列内容：
         - 计划的类型：
           - **小时** - 每隔多久运行一次计划：指定小时数和分钟数，以及开始时间。
           - **天** - 选择下面的三个选项之一：  
              - **于以下日期**：（周日、周一、周二、周三、周四、周五、周六）。
              - **每个工作日**
              - **重复执行间隔的天数**请指定一个数值。  
           - **周** - 同时指定下面的两个项：
              - **重复执行间隔的周数** - 请指定一个数值。  
              - **在某些天** - 选择在一周的某些天运行它。  
           - **月** - 哪些月份，可选择：
              - **在月中的以下周**：  
                 - 从下拉框选择（第一周、第二周、第三周、第四周或最后一周）。  
                 - **在一周的某些天**运行它。 选择一个或多个复选框（周一、周二、周三、周四、周五、周六、周日）。  
                 - **日历日** - 输入一个月中实际的第几天（使用逗号分隔）、日期范围（使用短划线分隔）或这两者的组合（如 1，3-5）。  
           - **一次** - 运行一次。  
         - **开始时间** - 计划开始的日期时间。  
         - **开始和结束日期** - 指定开始日期，并指定计划计划的结束日期（可选）。
         - 选择“应用”，保存计划。   
           > [!NOTE]
           > 如果该项未启用缓存，系统将会提示您启用缓存。 若要启用缓存，请选择  “确定”。  

         - 选择“创建缓存刷新计划”，来创建/保存缓存计划。   
         屏幕将打开“缓存刷新计划”页。  可以从此页执行下列操作：
           - 添加新缓存刷新计划。
           - 从现有计划新建缓存刷新计划。
           - 刷新缓存刷新计划页。
           - 删除计划。
           - 按名称搜索计划。

         若尚未保存任何缓存刷新计划，列表将为空，“添加”选项将是唯一可用的选项。 选择“+ 新建缓存刷新计划”添加新的计划，然后将显示“新建缓存刷新计划”页。    
           - 在第一个文本框键入说明，来为刷新计划命名。   
           - 从“按以下计划刷新缓存”选择下列单选按钮之一   
             - **共享计划** - 从相邻的下拉框中选择一个共享计划。 
             - **报表特定计划** - 如需查看“计划详细信息”页，请选择“编辑计划”链接，并按照上面的步骤 2.2 编辑计划。   
             - 添加后请选择“创建缓存刷新计划”保存计划，编辑计划后请选择“应用”。    
      你将返回到更新的“缓存刷新计划”页。 
  
## <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>通过使用数据驱动订阅将用户特定报表预加载到缓存中

1. 启动[报表服务器的 Web 门户](../../reporting-services/web-portal-ssrs-native-mode.md "报表服务器的 Web 门户")。  
2. 从主屏幕选择“浏览”，然后通过导航文件夹层次结构找到想要订阅的报表。   
3. 右键单击报表，从下拉菜单选择“订阅”。  将显示“新建订阅”页。   
4. 在“说明”文本框中输入订阅说明。   
5. “订阅类型”单选按钮显示两个选项：   
   - **标准订阅** - 将生成和传递一个报表
   - **数据驱动的订阅** - 为数据集中的每行生成和传递一个报表。 要预加载缓存时，请选择此选项。
6. 从“计划”部分选择以下单选按钮之一： 
   - **共享计划** - 从下拉框中选择一个共享计划。  
   - **报表特定计划** - 如需查看“计划详细信息”页，请选择“编辑计划”链接，并按照上面的步骤 2.2 编辑计划。    
7. “目标”部分将通过下拉框显示下列选项： 
    - **Windows 文件共享**
    - **电子邮件**
    - **Null 传递提供商** - 对于此任务，请选择“Null 传递提供商”。  
8. 从“数据集”部分中，选择“编辑数据集”按钮，来为此报表订阅编辑或创建数据集。    
9. 从“编辑数据集”页的“数据源”部分中，选择包含报表参数值和传递选项的数据源。   选项包括：  
   - **共享数据源** - 选择省略号，并从“共享数据源”  文件夹选择共享数据源。
   - **自定义数据源** - 选择它的可能性最高。 若你或其他人尚未完成下列步骤，来将其创建为共享数据源，则必须要选择此选项。  
     - 指定用于访问包含订阅服务器数据的数据源的连接类型、连接字符串和凭据。 以下示例演示用于连接到名为 Subscribers 的 SQL Server 数据库的连接字符串。  
  
   ```T-SQL
   data source=<servername>;initial catalog=Subscribers  
   ```
  
10. 从“查询”部分指定查询，来检索所需的订阅者数据。   例如：  
  
    ```T-SQL  
    Select * from RptSubscribers  
    ```
  
    对于处理时间很长的查询，可以根据需要延长超时期限。  
  
11. 选择“验证”。  在继续之前，必须验证查询。 显示“验证成功”消息时，“验证”按钮下方将显示数据集字段列表。   选择“应用”，创建自定义数据源。   
  
12. 你将返回到“新建订阅”页。   从“报表参数”部分为所显示的报表参数（如果有）指定报表参数值。   

13. 选择“创建订阅”。   
  
14. 将显示“订阅”页，其中说明了新的数据驱动的订阅。  准备就绪时，可以从此页选择左侧的复选框，然后选择“启用按钮”来启用此订阅。  ![“订阅”页的“启用”按钮](../../reporting-services/report-server/media/preload-the-cache/subscriptions-page-enable-button.png "“订阅”页上的“启用”按钮")

15. 指定处理订阅的时间。 不要选择“在报表服务器上更新报表数据时”  。 该设置仅适用于快照。 如果要使用预先存在的计划，请选择“根据共享计划”  。  
  
     若要创建自定义计划，请选择“根据为此订阅创建的计划”  ，再选择“下一步”  。 配置计划，再选择“完成”  。  
  
    > [!NOTE]  
    > 为确保订阅服务器能接收到最新的报表，所配置的计划应与为订阅服务器定义的报表传递计划相一致。 有关详细信息，请参阅[报表服务器的 Web 门户](../../reporting-services/web-portal-ssrs-native-mode.md  "报表服务器的 Web 门户")。  
  
16. 按照下面的步骤为报表配置执行选项。 在报表页上，选择“属性”  选项卡。  
  
17. 在左框架中，选择“执行”  选项卡。  
  
18. 在该页上，选择 **“用最新数据呈现此报表”** 。  
  
19. 选择如下两个缓存选项之一并配置过期时间：  
  
    - 若要使缓存的副本在特定的时间段后过期，请选择**缓存报表的临时副本。在数分钟之后使报表副本过期。”** 键入报表过期所需的分钟数。  
  
    - 若要按计划使缓存的副本过期，请选择“缓存报表的临时副本。  按下列计划使报表副本过期。” 选择“配置”  ，或选择一个共享计划以设置报表过期计划。  
  
20. 选择“应用”。 
  
## <a name="see-also"></a>另请参阅  

 [数据驱动订阅](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [创建数据驱动订阅（SSRS 教程）](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
 [性能、快照、缓存 (Reporting Services)](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)  
 [设置报表处理属性](../../reporting-services/report-server/set-report-processing-properties.md)  
 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [使用共享数据集](../../reporting-services/work-with-shared-datasets-web-portal.md)  
  
