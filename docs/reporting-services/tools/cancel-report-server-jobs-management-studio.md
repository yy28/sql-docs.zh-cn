---
title: "取消报表服务器作业 (Management Studio) |Microsoft 文档"
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
f1_keywords:
- sql13.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5348146e3cce3c1f3f6288797f8a4e2bbd520cab
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="cancel-report-server-jobs-management-studio"></a>取消报表服务器作业 (Management Studio)
  使用“取消报表服务器作业”对话框可以查看或取消正在执行的报表。 此对话框显示报表服务器上当前运行的所有作业。 尽管不能暂停或重新启动当前正在处理的作业，但是可以取消需要很长时间才能完成的所有作业或单个作业。  
  
 可以取消用户作业和系统作业。  
  
-   用户作业是由单个用户启动的任何作业。 这包括按需运行报表、手动创建报表历史记录快照或手动创建报表执行快照。 正在处理的标准订阅也是用户作业。  
  
-   系统作业是指由报表服务器启动的作业。 系统作业包括计划的报表处理。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器，右键单击“作业”，再单击“取消所有作业”。 还可以打开“作业”，右键单击报表服务器上正在运行的作业，然后选择“取消作业”。  
  
 在取消作业之前，可以查看其属性来确定作业的开始时间。 有关详细信息，请参阅[作业属性 (Management Studio)](../../reporting-services/tools/job-properties-management-studio.md)。  
  
> [!NOTE]  
>  在具有高级服务的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中不支持此功能。 运行 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]时，将不会显示该页。  
  
## <a name="options"></a>选项  
 **名称**  
 显示报表的名称。 订阅通过其各自的说明进行标识。  
  
 **类型**  
 有效值为 **User** 和 **System**。  
  
 **Start Time**  
 显示作业的开始时间。  
  
 **用户名**  
 对于由用户启动的作业，此列显示用户名。  
  
 **状态**  
 显示作业的状态。 有效值为 **“新”** 和 **“正在运行”**。 当作业开始时，状态始终为 **“新”** 。 在 60 秒之后，状态会改为 **“正在运行”**。 必须刷新该页才能看到变化。  
  
 **确定**  
 取消一个或多个作业。 作业会立即取消，并且不能恢复。 如果错误地取消了某个作业，则必须再次请求报表或订阅功能以启动新作业。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [在 Management Studio 中连接到报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [管理运行中的进程](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
