---
title: 作业属性：新建作业（"通知" 页） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8fafac7faaf98fd8cf9bd3b0bf772dc77324bae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062282"
---
# <a name="job-properties-new-job-notifications-page"></a>作业属性：新建作业（“通知”页）
  使用此页可以设置在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作业完成时代理要执行的操作。  
  
## <a name="options"></a>选项  
 **电子邮件**  
 选择此选项将在作业完成时发送电子邮件。 选择此选项后，选择要通知的操作员以及触发该通知的条件：“当作业成功时”****；“当作业失败时”****；或“当作业完成时”****。  
  
 **第**  
 选择此选项将在作业完成时将电子邮件发送到操作员的寻呼程序。 选择此选项后，指定要通知的操作员以及触发该通知的条件：“当作业成功时”****；“当作业失败时”****；或“当作业完成时”****。  
  
 **Net send**  
 选择此选项将在作业完成时通过 net send 通知操作员。 选择此选项后，指定要通知的操作员以及触发该通知的条件：“当作业成功时”****；“当作业失败时”****；或“当作业完成时”****。  
  
 **写入 Windows 应用程序事件日志**  
 选择此选项将在作业完成时将条目写入到应用程序事件日志中。 选择此选项后，指定导致写入条目的条件：“当作业成功时”****；“当作业失败时”****；或“当作业完成时”****。  
  
 **自动删除作业**  
 选择此选项将在作业完成时删除该作业。 选择此选项后，指定触发删除作业的条件：“当作业成功时”****；“当作业失败时”****；或“当作业完成时”****。  
  
## <a name="see-also"></a>另请参阅  
 [实现作业](implement-jobs.md)   
 [配置 SQL Server 代理邮件以使用数据库邮件](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
