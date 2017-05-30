---
title: "查看或修改作业 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fb14f6a9c778a48454a9f8d2e64f49d724558e88
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="view-or-modify-jobs"></a>查看或修改作业
您可以查看任何已创建的作业。 运行完一个作业后，还可以查看它的历史记录。 查看作业历史记录使您可以查看作业何时运行、整个作业的状态以及作业中每步作业的状态。 在作业成功完成后，您可以查看该作业过去是否曾失败，还可以查看作业每次运行时创建的输出内容。 **sysadmin** 固定服务器角色的成员可以查看或修改所有人的作业。  
  
> [!NOTE]  
> 作业至少必须运行一次，才会有作业历史记录。 您可以限制作业历史记录日志的总大小以及其中每个作业的大小。  
  
最后，您还可以修改作业以满足新的要求。 可以修改：  
  
-   响应选项  
  
-   计划  
  
-   作业步骤  
  
-   所有权  
  
-   作业类别  
  
-   目标服务器（仅适用于多服务器作业）  
  
为了确保对多服务器作业所做的更改生效，必须将这些更改发布到下载列表中，使目标服务器可以下载更新的作业。 若要确保目标服务器具有最新的作业定义，请在更新完多服务器作业后，按如下所示发布一条 INSERT 指令：  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
有关详细信息，请参阅 [sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88)。  
  
**sysadmin** 固定服务器角色的成员可以查看任何作业的定义或历史记录，还可以修改任何作业。  
  
## <a name="related-tasks"></a>相关任务  
  
|||  
|-|-|  
|**Description**|**主题**|  
|说明如何查看 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业。|[View a Job](../../ssms/agent/view-a-job.md)|  
|说明如何查看 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业历史记录日志。|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|说明如何删除 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业历史记录日志的内容。|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|说明如何设置 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业历史记录日志的大小限制。|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|说明如何更改 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业的属性。|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>另请参阅  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
  

