---
title: "“进度”页（AlwaysOn 可用性组向导）| Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 78fd0315e1f58eef1dbc5d8c41f6254817879d8c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="progress-page-always-on-availability-group-wizards"></a>“结果”页（Always On 可用性组向导）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用此对话框可以查看您在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中运行的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]向导的进度。 进度栏指示该向导正在执行的步骤的相对进度。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **更多详细信息**  
 单击下箭头可显示进度网格，其中按顺序列出所有已完成的步骤，后面跟有当前正在进行的操作。 该网格包含以下列：  
  
 **名称**  
 显示描述特定步骤的短语。  
  
 **状态**  
 指示已完成步骤的结果，以及当前步骤的完成百分比，如下所示：  
  
|结果|说明|  
|------------|-----------------|  
|**错误**|指示此步骤操作遇到了错误。 单击该链接可显示一个描述该错误的消息对话框。|  
|**正在进行（**完成百分比**）**|指示操作正在发生，并且估计此步骤已完成的百分比。|  
|**成功**|指示此步骤操作已成功完成。|  
  
 **更少详细信息**  
 单击此选项可隐藏进度网格。  
  
 **取消**  
 单击此选项可跳过剩下的所有操作，然后退出该向导。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用“将副本添加到可用性组向导”(SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [使用故障转移可用性组向导 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

