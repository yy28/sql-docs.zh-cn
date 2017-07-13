---
title: "使用快照 （web 门户） |Microsoft 文档"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ae20556-e243-4a60-b076-9fd9e82c7355
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 2bca4e3089bde763669c4fe518f509fbe94cb6eb
ms.contentlocale: zh-cn
ms.lasthandoff: 07/03/2017

---

# 使用快照（web 门户）
<a id="working-with-snapshots-web-portal" class="xliff"></a>

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

你可以控制如果为报表创建快照，应选择**省略号 （...）**的报表，请选择**管理**并选择**Caching**或**历史记录快照**。  
  
> [!NOTE]
> 需要启动 SQL Server 代理服务。  
   
可以创建缓存快照，以便可以更快地加载特定执行属性。 还可以使用历史记录快照捕获时间点。  
  
## 创建缓存快照
<a id="creating-a-cache-snapshot" class="xliff"></a>  
  
可以通过执行以下操作来创建快照。  
  
![ssRSWebPortal-report-caching4](../reporting-services/media/ssrswebportal-report-caching4.png)  
  
1.  在“缓存” 页上，选择“始终对预先生成的快照运行此报告”以启用用于创建快照的选项。  
  
2.  如果要计划定期快照，请选择“按计划创建缓存快照”。 然后可以使用共享计划，或定义自定义计划以刷新快照。  
  
3.  如果要立即创建缓存快照，请选择“当我在此页面上单击‘应用’时创建缓存快照”。 如果仅选择此选项，则不会刷新快照。  
  
## 创建、修改和删除历史记录快照
<a id="create-modify-and-delete-history-snapshots" class="xliff"></a>  
  
若要使用历史记录快照，请管理报表并选择“历史记录快照”。  
  
使用“历史记录快照”页可以查看一段时间中生成并存储的报表快照。 根据报表服务器上设置的选项，历史记录可能只包含较新的快照。  
  
报表历史记录总是显示在所源于的报表的上下文中。 您不能一起查看报表服务器中所有报表的历史记录。  
  
若要生成历史记录快照，报表必须能够以无人参与的方式运行（也就是说，报表必须使用存储的凭据；参数化报表必须包含所有参数的默认参数值）。 可以手动或以计划操作方式生成报表历史记录。 报表的历史记录属性决定报表历史记录的创建方式。  
  
![ssRSWebPortal-historysnapshots1](../reporting-services/media/ssrswebportal-historysnapshots1.png)  
   
1.  若要创建历史记录快照，请选择“+ 新历史记录快照”。 这会处理报表并向列表添加条目。  
  
2.  可以转到用于定义计划和保留策略的设置。  
  
3.  可以选择历史记录快照以查看它。 报表历史记录中显示的快照只能通过创建的日期和时间来区分。 无法通过直观方式判断出某个快照是为响应计划而生成的还是为响应某个手动操作而生成的。  
  
### 计划和设置
<a id="schedule-and-settings" class="xliff"></a>  
  
选择“计划和设置”将提供附加选项，用于计划和控制保持已创建快照的保留。  
  
![ssRSWebPortal-historysnapshots2](../reporting-services/media/ssrswebportal-historysnapshots2.png)  
   
可以选择创建计划，以便创建快照。 还可以阻止其他人创建新快照。 取消选中“允许用户手动创建快照”会禁用“+ 新快照历史记录”按钮。  
  
还可以定义要用于保留快照的方式。  
  
**同时将缓存快照保存在报表历史记录中**  
  
选择此项可以根据报表执行属性将生成的报表快照添加到报表历史记录中。 您可以设置报表执行属性以便从生成的快照运行报表。 设置此报表历史记录属性后，您可以将一段时间内生成的所有报表快照的副本放置在报表历史记录中，以跟踪这些报表快照。

## 后续步骤
<a id="next-steps" class="xliff"></a>

[Web 门户](../reporting-services/web-portal-ssrs-native-mode.md)  
[使用分页报表](working-with-paginated-reports-web-portal.md)  
[使用共享数据集](../reporting-services/work-with-shared-datasets-web-portal.md)

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
