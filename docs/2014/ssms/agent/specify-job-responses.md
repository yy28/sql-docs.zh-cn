---
title: 指定作业响应 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5365b0210fda978cd4425d4e621d9dcf7aefb928
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128012"
---
# <a name="specify-job-responses"></a>指定作业响应
  作业响应指定完成作业后 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务将执行的操作。 作业响应可确保数据库管理员知道作业完成的时间和作业运行频率。 典型的作业响应包括：  
  
-   使用电子邮件、电子寻呼或 **net send** 消息通知操作员。  
  
     如果操作员必须执行后续操作，应使用其中的某种作业响应。 例如，当一个备份作业成功地完成之后，必须通知操作员取出备份磁带并将其存放在安全处。  
  
-   将事件消息写入 Windows 应用程序日志。  
  
     只能对失败的作业使用这种响应。  
  
-   自动删除作业。  
  
     如果确信不需要再次运行该作业，可以使用这种作业响应。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Description**|**主题**|  
|描述如何向操作员通知作业状态。|[Notify an Operator of Job Status](notify-an-operator-of-job-status.md)|  
|介绍如何将作业状态写入 Windows 应用程序日志。|[Write the Job Status to the Windows Application Log](../../reporting-services/report-server/windows-application-log.md)|  
  
## <a name="see-also"></a>请参阅  
 [监视事件和响应事件](monitor-and-respond-to-events.md)  
  
  