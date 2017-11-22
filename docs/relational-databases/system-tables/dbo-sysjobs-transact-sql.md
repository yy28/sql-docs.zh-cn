---
title: "dbo.sysjobs (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fd6e90a9e823e38a83f5b218027e15183ab76ae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储将由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的各个预定作业的信息。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作业的唯一 ID。|  
|**originating_server_id**|**int**|发出作业的服务器的 ID。|  
|**名称**|**sysname**|作业的名称。|  
|**启用**|**tinyint**|指示是否启用要执行的作业。|  
|**说明**|**nvarchar(512)**|对作业的说明。|  
|**start_step_id**|**int**|执行作业的起始步骤的 ID。|  
|**category_id**|**int**|作业类别的 ID。|  
|**owner_sid**|**varbinary(85)**|作业所有者的安全标识号 (SID)。|  
|**notify_level_eventlog**|**int**|**位掩码**，该值指示应在什么情况下在 Microsoft Windows 应用程序日志中记录通知事件：<br /><br /> **0** = 从不<br /><br /> **1** = 作业成功时<br /><br /> **2** = 当作业失败时<br /><br /> **3** = 当作业完成 （不考虑作业结果中） 时|  
|**notify_level_email**|**int**|位掩码，指示在何种情况下应在作业完成时发送通知电子邮件：<br /><br /> **0** = 从不<br /><br /> **1** = 作业成功时<br /><br /> **2** = 当作业失败时<br /><br /> **3** = 当作业完成 （不考虑作业结果中） 时|  
|**notify_level_netsend**|**int**|位掩码，指示在何种情况下应在作业完成时发送网络消息：<br /><br /> **0** = 从不<br /><br /> **1** = 作业成功时<br /><br /> **2** = 当作业失败时<br /><br /> **3** = 当作业完成 （不考虑作业结果中） 时|  
|**notify_level_page**|**int**|位掩码，指示在何种情况下应在作业完成时发送寻呼：<br /><br /> **0** = 从不<br /><br /> **1** = 作业成功时<br /><br /> **2** = 当作业失败时<br /><br /> **3** = 当作业完成 （不考虑作业结果中） 时|  
|**notify_email_operator_id**|**int**|被通知的操作员的电子邮件名称。|  
|**notify_netsend_operator_id**|**int**|发送网络消息时使用的计算机或用户的 ID。|  
|**notify_page_operator_id**|**int**|发送寻呼时使用的计算机或用户的 ID。|  
|**delete_level**|**int**|**位掩码**，该值指示在什么情况下作业完成时应删除该作业：<br /><br /> **0** = 从不<br /><br /> **1** = 作业成功时<br /><br /> **2** = 当作业失败时<br /><br /> **3** = 当作业完成 （不考虑作业结果中） 时|  
|**date_created**|**datetime**|作业的创建日期。|  
|**date_modified**|**datetime**|上次修改作业的日期。|  
|**version_number**|**int**|作业版本。|  
  
  
