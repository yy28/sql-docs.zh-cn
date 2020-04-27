---
title: 计划属性（“报表”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 08fc68575e2515907f31e82cf3609d73da1c95d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099788"
---
# <a name="schedule-properties-reports-page"></a>计划属性（“报表”页）
  使用此页可以查看使用此共享计划的所有报表的列表。 计划可用于刷新报表快照、生成报表历史记录、触发订阅或使报表的缓存副本过期。 若要了解如何使用计划，请查看报表的属性和订阅信息。  
  
 尽管此页显示了所有使用共享计划的报表，但是它并没有说明共享计划在单个报表中的使用次数。 例如，假设 Company Sales 报表的 20 个不同的订阅均使用同一个共享计划来触发订阅处理。 在这种情况下，Company Sales 报表将仅在该列表中出现一次，即使该报表对共享计划引用了 20 次也是如此。  
  
 若要打开此页， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]请启动，连接到 Report Server，打开 "**共享**计划" 文件夹，右键单击共享计划，选择 "**属性**"，然后单击 "**报表**"。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关各个版本支持的功能列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅 SQL Server 2012 的各个[版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473)（。https://go.microsoft.com/fwlink/?linkid=232473)  
  
## <a name="options"></a>选项  
 **Folder**  
 指定报表的路径。  
  
 **报告**  
 指定使用该计划的报表的名称。  
  
## <a name="see-also"></a>另请参阅  
 [创建、修改和删除计划](../subscriptions/create-modify-and-delete-schedules.md)   
 [“计划”](../subscriptions/schedules.md)   
 [Management Studio F1 帮助中的报表服务器](report-server-in-management-studio-f1-help.md)   
 [在 Management Studio 中连接到报表服务器](connect-to-a-report-server-in-management-studio.md)   
 [配置报表的常规属性 &#40;报表管理器&#41;](../configure-general-properties-for-a-report-report-manager.md)  
  
  
