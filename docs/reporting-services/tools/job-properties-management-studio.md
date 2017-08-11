---
title: "作业属性 (Management Studio) | Microsoft Docs"
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
- sql13.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f138c5caef261757a4bce22cb84ebeb7a2a68b8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="job-properties-management-studio"></a>作业属性 (Management Studio)
  使用“作业属性”页可以在取消正在执行的报表或订阅之前查看相关信息。  
  
 若要打开此页，请启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，连接到报表服务器，然后打开 **“作业”** 文件夹。 右键单击正在运行的作业，然后单击“属性”。  
  
> [!NOTE]  
>  在具有高级服务的 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 中不支持此功能。 运行 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]时，将不会显示该页。  
  
## <a name="tasks"></a>“任务”  
 必须刷新该页以检索有关报表服务器上当前正在运行的作业的信息，才能查看有关作业的信息：  
  
1.  打开报表服务器文件夹。  
  
2.  右键单击“作业”，再单击“刷新”。  
  
3.  如果列出了某个作业，请右键单击它，再单击“属性”。  
  
## <a name="options"></a>选项  
 **作业 ID**  
 分配给正在处理的作业的 GUID。 该值是在每次运行报表或订阅时随机生成的。  
  
 **作业状态**  
 有效值为 **“新”** 和 **“正在运行”**。 当作业开始时，状态始终为 **“新”** 。 在 60 秒之后，状态会改为 **“正在运行”**。 必须刷新该页才能看到变化。  
  
 **作业类型**  
 有效值为 **User** 和 **System**。 用户作业是由单个用户启动的任何作业。 这包括按需运行报表、手动生成报表历史记录快照或手动创建报表执行快照。 正在处理的标准订阅也是用户作业。 系统作业是指由报表服务器启动的作业。 系统作业包括由计划触发的报表处理。  
  
 **作业操作**  
 对于报表，此列显示正在处理哪些报表执行进程。 此值始终为 **“呈现”**。  
  
 **作业说明**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]默认情况下不提供作业说明。  
  
 **服务器名称**  
 显示正在处理该作业的报表服务器的名称。 如果您配置了扩展部署，则此值将表明哪台服务器正在处理该作业。  
  
 **报表名称**  
 显示报表的名称。 订阅通过其各自的说明进行标识。  
  
 **报表路径**  
 显示报表在报表服务器文件夹层次结构中的路径。  
  
 **Start Time**  
 显示进程的开始时间。  
  
 **用户名**  
 对于由用户启动的进程，此列显示用户名。 对于系统作业，这是报表服务器的名称。  
  
## <a name="see-also"></a>另请参阅  
 [Management Studio F1 帮助中的报表服务器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [连接到在 Management Studio 中的报表服务器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [管理正在运行的进程](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
