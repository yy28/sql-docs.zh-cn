---
title: dbo.sysalerts (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 271452f516e231e22140664c049dacdaea5257a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个警报在表中各占一行。 警报是为响应事件而发送的消息。 警报可向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境之外转发消息，警报可以是电子邮件或寻呼消息。 警报还可以生成任务。  此表存储在**msdb**数据库。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|警报 ID。|  
|**名称**|**sysname**|警报名称。|  
|**event_source**|**nvarchar(100)**|事件源：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**event_category_id**|**int**|保留供将来使用。|  
|**event_id**|**int**|保留供将来使用。|  
|**message_id**|**int**|用户定义的消息 ID 或对引用**sysmessages**触发此警报的消息。|  
|severity|**int**|触发此警报的严重级别。|  
|**enabled**|**tinyint**|警报的状态：<br /><br /> **0** = 已禁用。<br /><br /> **1** = 启用。|  
|**delay_between_responses**|**int**|此警报的两个通知间的等待时间（以秒为单位）。|  
|**last_occurrence_date**|**int**|警报的上次发生（日期）。|  
|**last_occurrence_time**|**int**|警报的上次发生（时间）。|  
|**last_response_date**|**int**|警报的上次通知（日期）。|  
|**last_response_time**|**int**|警报的上次通知（时间）。|  
|**notification_message**|**nvarchar(512)**|与警报一起发送的其他信息。|  
|**include_event_description**|**tinyint**|位掩码表示是否通过电子邮件、 寻呼机或 Net send 发送事件描述。 请参阅下面的值的图表。|  
|**database_name**|**nvarchar(512)**|此警报必须在其中发生才能触发该警报的数据库。|  
|**event_description_keyword**|**nvarchar(100)**|为触发警报而必须匹配的错误模式。|  
|**occurrence_count**|**int**|此警报的发生次数。|  
|**count_reset_date**|**int**|天 （日期） 计数重置为**0**。|  
|**count_reset_time**|**int**|天计数的时间将重置为**0**。|  
|**job_id**|**uniqueidentifier**|此警报发生时执行的任务的 ID。|  
|**has_notification**|**int**|警报发生时接收电子邮件通知的操作员数。|  
|**flag**|**int**|保留。|  
|**performance_condition**|**nvarchar(512)**|保留。|  
|**category_id**|**int**|保留。|  
  
 ## <a name="remarks"></a>注释

下表显示的 include_event_description 位掩码值。 Dbo.sysalerts 返回的十进制值。 

|decimal | BINARY | 含义 |
|------|------|------|
|0 |0000 |任何消息 |
|1 |0001 |电子邮件 |
|2 |0010 |寻呼机 (pager) |
|3 |0011 |页导航和电子邮件 |
|4 |0100 |Net send |
|5 |0101 |Net send 和电子邮件 |
|6 |0110 |Net send 和页导航 |
|7 |0111 |Net send、 寻呼机和电子邮件 |
  
