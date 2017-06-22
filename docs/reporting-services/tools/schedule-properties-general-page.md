---
title: "计划属性 （常规页） |Microsoft 文档"
ms.custom: 
ms.date: 06/11/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.general.f1
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: eac0a7b5f1a8da128fc90700be9b91e9a38ad694
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="schedule-properties-general-page"></a>计划属性（“常规”页）
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 页中的 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 可查看或修改共享计划。 共享计划可以用于替代报表特定计划或订阅特定计划。 将在保存计划之后应用对计划进行的更改。 对计划进行编辑不会影响当前正在进行的作业。 如果要编辑正在使用的计划，则将允许完成从该计划触发的、当前正在处理的所有报表和订阅。  
  
 在一个计划中无法支持所有形式的频率组合。 例如，如果要在每周五的中午 12:00 和下午 4:00 运行报表，那么您必须创建两个每日计划，并指定运行日期为星期五，一个计划的开始时间为中午 12:00， 另一个计划的开始时间为下午 4:00。  
  
 计划处理过程以承载和处理计划的报表服务器的本地时间为准。  
  
 若要打开此页，请执行以下操作：
 1) 启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2) 连接到报表服务器。
 3) 展开“共享计划”文件夹。
 4) 右键单击共享计划，并选择“属性”。  
  
> [!NOTE]  
>并非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个版本均提供此功能；并且在运行不具有此功能的版本时，此页将不会出现。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为该共享计划指定名称。  
  
 **运行此计划的开始日期**  
 为此计划指定开始日期。  
  
 **此计划的结束日期**  
 为此计划指定过期日期。  
  
 **类型**  
 指定重复执行模式是主要基于小时、天、周、月还是仅运行一次。  
  
 **小时(重复执行模式)**  
 指定用于以小时为间隔运行计划操作（例如，每 6 小时运行一次报表）的选项。 可以按小时和分钟指定时间间隔。  
  
 **天(重复执行模式)**  
 指定用于以天为间隔运行计划操作（例如，每 2 天运行一次报表）的选项。 可以按天指定时间间隔，并指定希望计划运行的具体时间（小时和分钟）。  
  
 **周(重复执行模式)**  
 指定用于以周为间隔运行计划操作或需要按周重复执行操作时（例如，每隔一周运行一次报表）的选项。 可以指定每周计划，并指定希望计划运行的具体日期和时间（天、小时和分钟）。  
  
 **月(重复执行模式)**  
 指定用于以月为间隔运行计划操作或需要按月重复执行操作时的选项。 可以指定每月计划，并指定希望计划运行的具体日期和时间（天、小时和分钟）。 可以在计划中忽略特定的月份。  
  
 **一次**  
 指定只在特定的日期和时间运行一次的计划。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [创建、修改和删除计划](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [计划](../../reporting-services/subscriptions/schedules.md)  
  
  


