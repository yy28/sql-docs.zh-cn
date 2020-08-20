---
description: 数据库邮件消息处理对象
title: 数据库邮件消息处理对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
ms.openlocfilehash: e627bd6505d43737061d8fab34cc819d52c22106
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494544"
---
# <a name="database-mail-messaging-objects"></a>数据库邮件消息处理对象
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **msdb** 数据库是数据库邮件主机数据库。 此数据库包含数据库邮件的存储过程和消息处理对象。 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中带有数据库邮件配置向导，可用来启用数据库邮件、创建和管理配置文件和帐户以及配置数据库邮件选项。  
  
##  <a name="objects-in-msdb-database"></a><a name="ComponentsAndConcepts"></a>**msdb** 数据库中的对象  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] msdb **msdb** 。 不过，数据库邮件不使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 网络。 因此，用户不必创建 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 端点即可使用数据库邮件。 外部数据库邮件进程使用标准的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通信。  
  
 如果启用了数据库邮件，它将在 **msdb** 数据库中显示下列对象。  
  
 这些对象是数据库邮件在邮件主机数据库内的接口。 还会安装其他对象以执行上面列出的对象所提供的功能， 但是这些对象仅供内部使用。  
  
|名称|类型|描述|  
|----------|----------|-----------------|  
|[sysmail_allitems (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)|**视图**|列出已提交到数据库邮件的所有邮件。|  
|[sysmail_event_log (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)|**视图**|列出有关 [Database Mail External Program](../../relational-databases/database-mail/database-mail-external-program.md)行为的邮件。|  
|[sysmail_faileditems (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)|**视图**|有关数据库邮件无法发送的邮件的信息。|  
|[sysmail_mailattachments (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)|**视图**|有关数据库邮件附件的信息。|  
|[sysmail_sentitems (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)|**视图**|有关已使用数据库邮件发送的邮件的信息。|  
|[sysmail_unsentitems (Transact-SQL)](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)|**视图**|有关数据库邮件当前正在尝试发送的邮件的信息。|  
|[sp_send_dbmail (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)|**存储过程**|使用数据库邮件发送电子邮件。|  
|[sysmail_delete_log_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|**存储过程**|从数据库邮件日志中删除邮件。|  
|[sysmail_delete_mailitems_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)|**存储过程**|从数据库邮件队列中删除邮件项。|  
|[sysmail_help_status_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql.md)|**存储过程**|指示数据库邮件是否已启动。|  
|[sysmail_start_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)|**存储过程**|启动外部程序使用的 Service Broker 对象。 默认情况下将会启动这些对象。|  
|[sysmail_stop_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)|**存储过程**|停止外部程序使用的 Service Broker 对象。|  
  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
