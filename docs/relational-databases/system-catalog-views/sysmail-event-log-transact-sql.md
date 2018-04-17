---
title: sysmail_event_log (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2f9818bda47d9e0ffac256220f36efa1c5c6360
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库邮件系统返回的每个 Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 消息都在视图中占一行。 （该上下文中的消息是指错误消息之类的消息，而不是电子邮件。）配置**日志记录级别**参数使用**配置系统参数**对话框中的数据库邮件配置向导，或[sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)存储过程，以确定哪些消息返回。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|日志中项的标识符。|  
|**event_type**|**varchar(11)**|插入日志中的通告的类型。 可能值为错误、警告、信息性消息、成功消息以及其他内部消息。|  
|**log_date**|**datetime**|记录日志条目的日期和时间。|  
|**说明**|**nvarchar(max)**|要记录的消息的文本。|  
|**process_id**|**int**|数据库邮件外部程序的进程 ID。 每当数据库邮件外部程序启动时，该进程 ID 通常都会更改。|  
|**mailitem_id**|**int**|邮件队列中邮件项的标识符。 如果消息与特定的电子邮件项不相关，则该值为 NULL。|  
|**account_id**|**int**|**Account_id**与事件相关的帐户。 如果消息与特定的帐户不相关，则该值为 NULL。|  
|**last_mod_date**|**datetime**|上次修改行的日期和时间。|  
|**last_mod_user**|**sysname**|上次修改行的用户。 对于电子邮件，这是发送邮件的用户。 对于数据库邮件外部程序生成的消息，这是程序的用户上下文。|  
  
## <a name="remarks"></a>注释  
 进行疑难解答时数据库邮件，搜索**sysmail_event_log**与电子邮件失败相关的事件视图。 某些消息（例如，数据库邮件外部程序的失败）并不与特定的电子邮件相关。 若要搜索与特定的电子邮件相关的错误，查找**mailitem_id**中失败的电子邮件的**sysmail_faileditems**查看，然后搜索**sysmail_event_log**与该订阅相关的消息**mailitem_id**。 当从返回错误**sp_send_dbmail**、 电子邮件时不会提交到数据库邮件系统和错误不会显示在此视图。  
  
 如果单个帐户传递尝试失败，则在重试过程中数据库邮件将会包含错误消息，直到邮件项传递成功或者失败为止。 发生 ultimate 成功后，所有用户计划累积的错误记录为单独的警告包括**account_id**。 这样，即使电子邮件已被发送，也会出现警告。 Ultimate 传送失败，发生所有以前的警告获取记录为一个错误消息，而**account_id**，因为所有帐户已都失败。  
  
## <a name="permissions"></a>权限  
 您必须是属于**sysadmin**固定的服务器角色或**DatabaseMailUserRole**数据库角色以访问此视图。 成员**DatabaseMailUserRole**不是成员的**sysadmin**角色，可以仅查看为在提交的电子邮件事件。  
  
## <a name="see-also"></a>另请参阅  
 [sysmail_faileditems &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [数据库邮件外部程序](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
