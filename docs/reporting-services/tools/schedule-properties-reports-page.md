---
title: 计划属性（“报表”页）| Microsoft Docs
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e8441dec655398ec530bc95049a339edd9e01ab
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "65571407"
---
# <a name="schedule-properties-reports-page"></a>计划属性（“报表”页）
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 计划属性页以查看使用特定共享计划的所有报表的列表。 计划可用于刷新报表快照、生成报表历史记录、触发订阅或使报表的缓存副本过期。 若要了解如何使用计划，请查看报表的属性和订阅信息。  
  
 尽管此页显示了所有使用共享计划的报表，但是它并没有说明共享计划在单个报表中的使用次数。 例如，假设 Company Sales 报表的 20 个不同的订阅均使用同一个共享计划来触发订阅处理。 在这种情况下，Company Sales 报表将仅在该列表中出现一次，即使该报表对共享计划引用了 20 次也是如此。  
  
 若要打开计划属性页：
 1. 启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2. 连接到报表服务器。
 3. 打开“共享计划”文件夹  。
 4. 右键单击共享计划，选择“属性”  。
 5. 单击“报表”  。  
  
  还可以从 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web 门户的“站点设置”管理共享计划。
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本支持的功能列表，请参阅 [SQL Server 2017 的各版本和支持的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
## <a name="options"></a>选项  
 **文件夹**  
 指定报表的路径。  
  
 **Report**  
 指定使用该计划的报表的名称。  
  
## <a name="see-also"></a>另请参阅  
 [创建、修改和删除计划](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [“计划”](../../reporting-services/subscriptions/schedules.md)   
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [配置报表的常规属性（报表管理器）](https://msdn.microsoft.com/10b941b2-28e6-4408-9ee4-acebc63c8496)  
  
  

