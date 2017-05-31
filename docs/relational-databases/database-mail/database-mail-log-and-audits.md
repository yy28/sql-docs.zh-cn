---
title: "数据库邮件日志和审核 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae64a6ae76dd4f5dd72e0e8815d509184ddf4503
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="database-mail-log-and-audits"></a>数据库邮件日志和审核
  数据库邮件日志记录功能旨在提供一种隔离和更正问题的方法。 数据库邮件将日志信息存储在 **msdb** 数据库中。 有关数据库邮件电子邮件内容的信息、电子邮件状态以及已接收的任何消息（例如，数据库邮件记录的错误）可用于故障排除和审核目的。  
  
## <a name="database-mail-logs"></a>数据库邮件日志  
 **msdb** 数据库中的表用于记录来自 [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md)的信息。 [数据库邮件视图 (Transact SQL)](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) 公开这些表以进行故障排除。 如果 Service Broker 不能激活外部程序、外部程序遇到网络错误或者简单邮件传输协议 (SMTP) 服务器拒绝电子邮件，[sysmail_event_log (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) 视图中就会显示错误。 如果外部程序无法将错误记录到 **msdb** 表，则会将错误记录到 Windows 应用程序事件日志。  
  
 **msdb** 数据库的内部表包含从数据库邮件发送的电子邮件和附件以及每封邮件的当前状态。 每封邮件被处理后，数据库邮件就会更新这些表。  
  
## <a name="database-mail-auditing-tasks"></a>数据库邮件审核任务  
  
|||  
|-|-|  
|**查看和管理数据库邮件日志**|**指向主题的链接**|  
|检查各个邮件的传递状态|[检查使用数据库邮件发送的电子邮件的状态](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|清理数据库邮件消息、附件和日志条目|[sysmail_delete_mailitems_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|存档数据库邮件和日志|[创建 SQL Server 代理作业以存档数据库邮件和事件日志](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
