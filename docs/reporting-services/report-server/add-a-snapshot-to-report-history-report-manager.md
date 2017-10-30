---
title: "将快照添加到报表历史记录 （报表管理器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report history [Reporting Services], adding snapshots
- historical data [Reporting Services]
- snapshots [Reporting Services], adding report snapshots
- adding snapshots to report history
- report snapshots [Reporting Services], adding
ms.assetid: 3aafb183-789e-46ac-966c-881dc549b31d
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5d340621db8dc12cd981d75939babeff40e590f2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-snapshot-to-report-history-report-manager"></a>向报表历史记录添加快照（报表管理器）
  报表历史记录是随着时间变化而创建的报表快照的集合。 报表快照是包含在特定时间点检索到的布局信息以及查询结果的报表。 与按需运行报表（在选择该报表时可获得最新的查询结果）不同，报表快照按计划进行处理，再保存到报表服务器中。 当您选择报表快照进行查看时，报表服务器将在报表服务器数据库中检索存储的报表，然后显示快照创建时报表的数据和布局。  
  
 报表快照不以特定的呈现格式进行保存。 相反，将以用户或应用程序发出请求时的最终查看格式（如 HTML）来呈现报表快照。 延迟呈现会使快照具有可移植性。 报表可以采用适用于请求设备或 Web 浏览器的正确格式呈现。  
  
### <a name="to-manually-add-snapshots-to-report-history"></a>向报表历史记录中手动添加快照  
  
1.  在报表管理器中，导航到**内容**页上，并将鼠标悬停在你想要查看历史记录，然后单击下拉箭头的项。  
  
2.  在下拉菜单中，单击 **“查看报表历史记录”**。  
  
3.  单击 **“新建快照”**。 将在 **“运行时间”** 列中创建一个新快照。  
  
    > [!NOTE]  
    >  为此，管理员必须将报表历史记录配置为 **“允许手动创建历史记录”**。 有关详细信息，请参阅 [限制报表历史记录（报表管理器）](../../reporting-services/reports/limit-report-history-report-manager.md)。  
  
4.  单击 **“应用”**。  
  
### <a name="to-automatically-add-all-snapshots-to-report-history"></a>自动向报表历史记录中添加所有快照  
  
1.  对于已配置为作为报表执行快照运行的报表，可以设置其他属性以在每次刷新该快照时将该快照的副本保存到报表历史记录。  
  
2.  在报表管理器中，导航到**内容**页上，将鼠标悬停在你想要查看历史记录，然后单击下拉箭头的项。  
  
3.  在下拉菜单中，单击 **“管理”**。  
  
4.  单击 **“快照选项”**。  
  
5.  选中 **“在历史记录中存储所有报表执行快照”**复选框。  
  
6.  单击 **“应用”**。  
  
### <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>基于计划自动向报表历史记录中添加快照  
  
1.  在报表管理器中，导航到**内容**页上，并将鼠标悬停在你想要查看历史记录，然后单击下拉箭头的项。  
  
2.  在下拉菜单中，单击 **“管理”**。  
  
3.  单击 **“快照选项”**。  
  
4.  选中 **“使用以下计划将快照添加到报表历史记录中”**复选框。 执行下列操作之一：  
  
    -   选择**报表特定计划**。 填入计划详细信息，选择计划的开始日期和结束日期，再单击 **“确定”**。  
  
    -   选择 **“共享计划”**。 从列表中选择首选计划。  
  
5.  单击 **“应用”**。  
  
## <a name="see-also"></a>另请参阅  
 [配置报表的执行属性（报表管理器）](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)   
 [打开和关闭报表 &#40;报表管理器 &#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [限制报表历史记录 &#40;报表管理器 &#41;](../../reporting-services/reports/limit-report-history-report-manager.md)   
 [计划](../../reporting-services/subscriptions/schedules.md)   
 [报表管理器 &#40;SSRS 本机模式 &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  

