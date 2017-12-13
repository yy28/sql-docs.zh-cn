---
title: "指定作业响应 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a95f0e289dd73b2001b7cb60d7ef707f9a26fd15
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="specify-job-responses"></a>指定作业响应
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 作业响应指定完成作业后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务将执行的操作。 作业响应可确保数据库管理员知道作业完成的时间和作业运行频率。 典型的作业响应包括：  
  
-   使用电子邮件、电子寻呼或 **net send** 消息通知操作员。  
  
    如果操作员必须执行后续操作，应使用其中的某种作业响应。 例如，当一个备份作业成功地完成之后，必须通知操作员取出备份磁带并将其存放在安全处。  
  
-   将事件消息写入 Windows 应用程序日志。  
  
    只能对失败的作业使用这种响应。  
  
-   自动删除作业。  
  
    如果确信不需要再次运行该作业，可以使用这种作业响应。  
  
## <a name="related-tasks"></a>相关任务  
  
|||  
|-|-|  
|**Description**|**主题**|  
|描述如何向操作员通知作业状态。|[Notify an Operator of Job Status](../../ssms/agent/notify-an-operator-of-job-status.md)|  
|介绍如何将作业状态写入 Windows 应用程序日志。|[Write the Job Status to the Windows Application Log](../../ssms/agent/write-the-job-status-to-the-windows-application-log.md)|  
  
## <a name="see-also"></a>另请参阅  
[监视事件和响应事件](../../ssms/agent/monitor-and-respond-to-events.md)  
  
