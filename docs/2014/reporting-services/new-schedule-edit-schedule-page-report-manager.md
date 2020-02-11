---
title: 新计划： "编辑计划" 页（报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 52a4d250-e185-4116-a29c-d809940a00fb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea1eed70c3eac8bac1c4141628e72ce0af8099c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108148"
---
# <a name="new-schedule-edit-schedule-page-report-manager"></a>新计划： "编辑计划" 页（报表管理器）
  使用“新建计划”/“编辑计划”页可为报表创建计划。 您可以与订阅一起使用计划，以刷新缓存的报表，以及按独立项的形式创建快照或在报表历史记录中创建快照。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅 SQL Server 2014 的各个[版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 您只能为以无人参与的方式运行的报表创建计划。 若要以无人参与方式运行报表，您需要将报表数据源凭据存储到报表服务器数据库中。 有关详细信息，请参阅 "[数据源属性" 页 &#40;报表管理器&#41;](../../2014/reporting-services/data-sources-properties-page-report-manager.md)。  
  
 在一个计划中无法支持所有形式的频率组合。 例如，如果要在每周五的中午 12:00 和下午 4:00 运行报表，那么您必须创建两个每日计划，并指定运行日期为星期五，一个计划的开始时间为中午 12:00， 另一个计划的开始时间为下午 4:00。  
  
 计划处理过程以承载和处理计划的报表服务器的本地时间为准。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-execution-properties-page-of-a-report"></a>从报表的“执行属性”页打开“新建计划”或“编辑计划”页  
  
1.  打开报表管理器，找到要配置计划的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”** 。 这会打开该模型的“常规属性”页。  
  
4.  选择 **“执行”** 选项卡。  
  
5.  选择 **“通过报表执行快照呈现此报表”** 选项。 然后，选择 **“使用以下计划将快照添加到报表历史记录中”**，并选择 **“报表特定计划”**。 然后，单击 **“配置”**。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-history-properties-page-of-a-report"></a>从报表的“历史记录属性”页打开“新建计划”或“编辑计划”页  
  
1.  打开报表管理器，找到要配置计划的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击 **“管理”** 。 这会打开该模型的“常规属性”页。  
  
4.  选择 **“历史记录”** 选项卡。  
  
5.  选择 **“使用以下计划将快照添加到报表历史记录中”**，并选择 **“报表特定计划”**。 然后，单击 **“配置”**。  
  
### <a name="to-open-the-new-schedule-or-edit-schedule-page-from-the-subscriptions-page"></a>从“订阅”页打开“新建计划”或“编辑计划”页  
  
1.  打开报表管理器，找到要配置计划的报表。  
  
2.  悬停在该报表之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，  
  
    -   单击“管理”。**** 这会打开该报表的“常规”属性页。 然后，选择 **“订阅”** 选项卡。  
  
    -   单击 **“订阅”**。 这会打开该报表的 **“订阅”** 属性页。  
  
4.  在工具栏中，单击 **“新建订阅”** 或选择要编辑的现有订阅。  
  
5.  在 **“订阅处理选项”** 下，单击 **“新建计划”**。  
  
## <a name="options"></a>选项  
 **计划详细信息**  
 选择决定运行报表的时间和频率的选项。 频率选项分为几级。 第一组选项指定频率的类别（每小时、每天、每周等）。 第二组选项的显示由初始选择决定。  
  
-   **小时**定义按小时时间间隔运行的计划。 使用 **“开始日期和结束日期”** 部分可以指定运行计划的日期。  
  
-   **Day**定义按特定的小时和分钟运行的计划。 您可以按以下方式指定日期： \<*每天>、每个工作日*和每\<个*数字*> 天。 选择一个选项会禁用其他选项，即使其他天已显示为选中状态也是如此。  
  
-   **周**定义按每周时间间隔在特定的小时和分钟运行的计划。 时间间隔可以是完整的周（例如，每两周）或一周中的几天。  
  
-   **Month**定义按月运行的计划。 在一个月中，您可以基于某种模式选择一天（如每个月最后一个星期日）或选择特定日期（如 1 和 15，表示每个月的第 1 天和第 15 天）。 可以通过使用逗号和连字符指定多个日期和范围，例如 1, 5, 7-12, 21。  
  
-   **定义只运行一次的**计划。 使用 **“开始日期和结束日期”** 部分可以指定运行计划的日期。 计划处理完后即过期。  
  
 **“开始日期和结束日期”**  
 通过此选项可以指定开始日期（确定计划何时生效）和结束日期（确定计划何时过期）。  
  
 计划过期时并无通知。 结束日期后，计划将不再运行。 过期的计划不会被删除。 只能手动删除这些计划。 也就是说，如果选择继续过期的计划，只需扩展结束日期即可。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [创建、修改和删除计划](subscriptions/create-modify-and-delete-schedules.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
