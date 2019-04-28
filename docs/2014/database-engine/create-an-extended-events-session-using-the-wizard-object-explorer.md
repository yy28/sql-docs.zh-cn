---
title: 创建扩展的事件会话使用向导 （对象资源管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc69e3683656c5705e7e82df27b80a8a41cb81a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807359"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>使用向导创建扩展事件会话（对象资源管理器）
  为了帮助您选择和捕获服务器上的事件，扩展事件包括一个“新建会话”向导，引导您完成创建扩展事件会话所需的步骤。 “新建会话”向导公开大多数扩展事件功能。 通过[“新建会话”对话框](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)，还可以定义捕获、显示和分析数据的扩展事件会话。 “新建会话”对话框公开所有扩展事件功能。  
  
### <a name="to-open-the-new-session-wizard"></a>打开“新建会话”向导  
  
1.  在对象资源管理器中，依次展开 **“管理”** 节点和 **“扩展事件”**。  
  
2.  右键单击“会话”，然后单击“新建会话向导”。  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>使用以下“新建会话”向导页可以创建事件会话  
  
-   [简介](#BKMK_Welcome)  
  
-   [设置会话属性](#BKMK_SetSessionProperties)  
  
-   [选择模板](#BKMK_ChooseTemplate)  
  
-   [选择要捕获的事件](#BKMK_SelectEventsToCapture)  
  
-   [捕获全局字段](#BKMK_CaptureGlobalFields)  
  
-   [设置会话事件筛选器](#BKMK_SetSessionEventFilters)  
  
-   [指定会话数据存储](#BKMK_SpecifySessionDataOutput)  
  
-   [摘要](#BKMK_Summary)  
  
-   [创建事件会话](#BKMK_CreateEventSession)  
  
##  <a name="BKMK_Welcome"></a> 简介  
 在 **“简介”** 页上，执行以下操作：  
  
-   在“新建会话”向导的 **“简介”** 页上，单击 **“下一步”**。  
  
     如果要多次使用该向导并且不想每次启动该向导时都阅读此简介，则选中“不再显示此页”复选框。  
  
##  <a name="BKMK_SetSessionProperties"></a> 设置会话属性  
 在 **“设置会话属性”** 页上，执行以下操作：  
  
-   在 **“会话名称”** 框中，键入事件会话的有意义的名称。  
  
     如果您想要在启动服务器时启动会话，则选中 **“在服务器启动时启动事件会话”** 复选框，然后单击 **“下一步”**。  
  
##  <a name="BKMK_ChooseTemplate"></a> 选择模板  
 在 **“选择模板”** 页上，执行以下操作：  
  
-   选择“使用此事件会话模板”选项可以从为常见问题设计的一组预先配置的模板中进行选择。 从下拉列表中选择你要使用的模板，然后单击“下一步”。  
  
     -或-  
  
-   如果你不想使用任何预先配置的模板，则选择“不使用模板”选项，然后单击“下一步”。  
  
##  <a name="BKMK_SelectEventsToCapture"></a> 选择要捕获的事件  
 在 **“选择要捕获的事件“** 页上，执行以下操作：  
  
1.  从 **”事件库“** 中选择要使用的事件，然后单击向右箭头。 您可以通过使用 Shift+单击或 Ctrl+单击在事件库中选择多个事件。  
  
     您可以从下拉列表框中选择搜索要捕获的事件的方式。 例如，您可以搜索事件名称或者事件名称及其说明。 您可以通过在 **“事件库”** 框中输入要搜索的文本，搜索表中的任何词语。 例如，如果你想要查找 **lock_acquired** 事件，则可以输入 **lock**或 **lock acquire**。  
  
     您选择的事件将出现在 **“所选事件”** 框中。 若要从 **“所选事件”** 框中删除事件，请单击向左箭头。  
  
2.  在选择了要捕获的事件后，单击 **“下一步”**。  
  
    > [!NOTE]  
    >  默认情况下将隐藏来自 **“调试”** 渠道的事件。 若要显示调试事件，请从“渠道”下拉列表中选择“调试”。  
  
##  <a name="BKMK_CaptureGlobalFields"></a> 捕获全局字段  
 使用全局字段（也称作操作）可以关联所选事件的单个或多个操作。 如果您在 **“选择模板”** 页上选择了某个模板，则在该模板中定义的所有全局字段都将显示在此页上。  
  
 在 **“捕获全局字段“** 页上，执行以下操作：  
  
-   选择您要为事件会话捕获的全局字段，然后单击 **“下一步”**。  
  
     您可以通过选中或取消选中全局字段旁的复选框，删除或添加全局字段。  
  
    > [!NOTE]  
    >  所选操作将按 **“名称”** 排序，这样，您可以按字母顺序查看关联的操作。 您可以通过单击字段名称旁的列标题，按照说明或者启用/禁用状态进行排序。  
  
##  <a name="BKMK_SetSessionEventFilters"></a> 设置会话事件筛选器  
 您可以应用筛选器（也称作谓词）来限制要捕获的事件。 在 **“设置事件筛选器”** 页上，执行以下操作：  
  
1.  如果你未在使用预先配置的模板，则创建你的筛选条件，然后单击“下一步”。  
  
     如果你正在使用某个预先配置的模板，则在“来自模板的筛选器(只读)”部分中，“新建会话”向导将列出已根据该模板创建的筛选器。  
  
2.  在 **“附加筛选器”** 部分中，您可以配置事件会话的附加筛选器。  
  
     您配置的筛选器将应用于所有所选事件。 “新建会话”向导不支持为每个事件都配置筛选器。  
  
    > [!NOTE]  
    >  在您为筛选器配置组子句时，在保存结果后多余的括号将从筛选器中删除。 例如，如果您创建一个筛选器分组 **Clause 1** 和 **Clause 2**，则括号会将这两个子句括起来。 在您保存筛选器后，多余的括号将被删除。 删除这些括号不会影响筛选器逻辑。  
  
##  <a name="BKMK_SpecifySessionDataOutput"></a> 指定会话数据存储  
 使用 **“指定会话数据存储”** 页可以指定您要收集数据以便进行分析的方式。 SQL Server 扩展事件使用目标进行数据输出。 目标存储事件数据并且可以执行各种操作，例如写入文件和聚合事件数据。 决定您要收集数据以便进行分析的方式，并且在 **“指定会话数据存储”** 页上，执行以下操作：  
  
1.  对于大型数据集和创建历史记录，请选中 **“将数据保存到文件以便以后分析”** 复选框，然后执行以下操作：  
  
    1.  在 **“服务器上的文件名”** 框中，输入路径和文件名，或者单击 **“浏览”** 以便指定服务器上您要用于保存数据的文件目录。  
  
    2.  在 **“最大文件大小”** 框中，指定要用于文件目标的最大文件大小。 如果未指定最大文件大小，则文件将一直增长到磁盘变满为止。 默认文件大小为 1 GB。  
  
    3.  选中 **“启用文件滚动更新”** 复选框可为文件目标启用文件滚动更新。  
  
    4.  在 **“最大文件数”** 框中，指定您要在文件系统中保留的最大文件数。  
  
2.  若要收集最近的数据，请选中“仅使用最近数据(环形缓冲区目标)”复选框，然后执行以下操作：  
  
    1.  在 **“要保留的事件数目”** 框中，通过使用向上和向下箭头输入或选择您要保留的事件数目。  
  
    2.  在 **“最大缓冲区内存大小”** 框中，指定要使用的缓冲区内存的最大大小。 达到此值时将删除现有事件。  
  
    3.  如果你想要在缓冲区中保留每种类型的特定的事件数目，则选中“在缓冲区已满时保留指定数目的事件(按类型)”复选框。  
  
    4.  在“要保留的事件数目(按类型)”框中，通过使用向上和向下箭头输入或选择你要保留的事件数目（按类型）。  
  
##  <a name="BKMK_Summary"></a> 摘要  
 在 **“摘要”** 页上，执行以下操作：  
  
1.  请确保您的选择是正确的。 展开事件会话节点以便确认您的所有选择都包括在事件会话中。  
  
2.  单击 **“脚本”** 以便将会话创建脚本导出到新的查询编辑器窗口中。  
  
3.  单击 **“完成”** 以便创建事件会话。  
  
##  <a name="BKMK_CreateEventSession"></a> 创建事件会话  
 在 **“创建事件会话”** 页上，在已成功创建您的事件会话后，执行以下操作：  
  
1.  单击 **“在会话创建后立即启动事件会话”** 以便在您关闭向导后启动会话。 您必须在创建会话后立即启动事件会话，以便能够查看实时数据。  
  
2.  单击 **“在捕获时查看屏幕上的实时数据”** 可以查看您的事件会话的实时数据。 实时数据将在创建会话后立即开始显示跟踪。  
  
## <a name="see-also"></a>请参阅  
 [使用“新建会话”对话框创建扩展事件会话](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  
