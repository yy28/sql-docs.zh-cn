---
title: sysmail_sentitems (TRANSACT-SQL) |Microsoft 文档
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
- sysmail_sentitems_TSQL
- sysmail_sentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_sentitems database mail view
ms.assetid: 16eb2a44-cebb-4cec-93ac-e2498c39989f
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f65f33de438152843839853d9e53dff9154f7ae7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailsentitems-transact-sql"></a>sysmail_sentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库邮件发送的每个消息都在视图中占一行。 使用**sysmail_sentitems**当你想要查看哪些消息发送成功。  
  
 若要查看通过数据库邮件处理的所有消息，使用[sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)。 若要查看仅具有失败的状态消息，使用[sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)。 若要查看仅未发送或重试消息，使用[sysmail_unsentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)。 若要查看电子邮件附件，使用[sysmail_mailattachments &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|邮件队列中邮件项的标识符。|  
|**profile_id**|**int**|发送消息所用配置文件的标识符。|  
|**收件人**|**varchar(max)**|消息收件人的电子邮件地址。|  
|**copy_recipients**|**varchar(max)**|接收消息副本的用户的电子邮件地址。|  
|**blind_copy_recipients**|**varchar(max)**|接收消息副本但其姓名未出现在消息标头中的用户的电子邮件地址。|  
|**subject**|**nvarchar(510)**|消息的主题行。|  
|**正文**|**varchar(max)**|消息的正文。|  
|**body_format**|**varchar(20)**|消息正文的格式。 可能的值为**文本**和**HTML**。|  
|**重要性**|**varchar(6)**|**重要性**消息参数。|  
|**敏感度**|**varchar(12)**|**敏感度**消息参数。|  
|**file_attachments**|**varchar(max)**|附加到电子邮件中的文件名列表，以分号分隔。|  
|**attachment_encoding**|**varchar(20)**|邮件附件的类型。|  
|**查询**|**varchar(max)**|邮件程序所执行的查询。|  
|**execute_query_database**|**sysname**|邮件程序在其中执行查询的数据库上下文。|  
|**attach_query_result_as_file**|**bit**|如果该值为 0，则查询结果包含在电子邮件的正文中，在正文的内容之后。 如果该值为 1，则结果作为附件返回。|  
|**query_result_header**|**bit**|值为 1 时，查询结果将包含列标题。 0 值时，查询结果未包含列标题。|  
|**query_result_width**|**int**|**Query_result_width**消息参数。|  
|**query_result_separator**|**char(1)**|用于分隔查询输出中的各列的字符。|  
|**exclude_query_output**|**bit**|**Exclude_query_output**消息参数。 有关详细信息，请参阅[sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。|  
|**append_query_error**|**bit**|**Append_query_error**消息参数。 0 指示如果查询中存在错误，则数据库邮件不应发送电子邮件。|  
|**send_request_date**|**datetime**|将消息放在邮件队列中的日期和时间。|  
|**send_request_user**|**sysname**|发送消息的用户。 这是数据库邮件过程的用户上下文，不是邮件的“发件人:”字段。|  
|**sent_account_id**|**int**|发送消息所用数据库邮件帐户的标识符。|  
|**sent_status**|**varchar(8)**|邮件的状态。 始终**发送**此视图。|  
|**sent_date**|**datetime**|发送消息的日期和时间。|  
|**last_mod_date**|**datetime**|上次修改行的日期和时间。|  
|**last_mod_user**|**sysname**|上次修改行的用户。|  
  
## <a name="remarks"></a>注释  
 排除数据库邮件故障时，该视图通过向您显示已成功发送的消息的属性，可帮助您确定问题的本质。 如果消息成功提交到 SMTP 邮件服务器，则数据库邮件将这些消息标记为已发送。 通常可在几分钟后收到电子邮件，但也可能由于 SMTP 服务器的问题而使电子邮件的接收延迟。 如果 SMTP 邮件服务器接受了消息，则数据库邮件将该消息标记为已发送。 SMTP 邮件服务器中出现的电子邮件错误（例如，无法传递的收件人电子邮件地址）不会返回到数据库邮件。 即使这些电子邮件未被传递，也会将它们记录为已发送。 请解决 SMTP 服务器中的此类错误。 此外，SMTP 邮件服务器还可能将无法传递的消息通知发送到数据库邮件帐户的答复电子邮件地址。  
  
## <a name="permissions"></a>权限  
 授予**sysadmin**固定的服务器角色和**databasemailuserrole**数据库角色。 由的成员执行时**sysadmin**固定服务器角色，此视图显示所有发送的消息。 所有其他用户仅可查看他们已发送的消息。  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件消息处理对象](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
  
