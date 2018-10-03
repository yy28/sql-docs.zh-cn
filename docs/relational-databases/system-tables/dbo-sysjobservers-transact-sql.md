---
title: dbo.sysjobservers (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobservers
- sysjobservers_TSQL
- dbo.sysjobservers
- dbo.sysjobservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobservers system table
ms.assetid: 9abcc20f-a421-4591-affb-62674d04575e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 635c71efaeed6d41a9b9e62ef3e8c79b4e9aae95
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607275"
---
# <a name="dbosysjobservers-transact-sql"></a>dbo.sysjobservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储特定作业与一个或多个目标服务器的关联或关系。此表存储在 msdb 数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|job_id|**uniqueidentifier**|作业标识号。|  
|server_id|**int**|服务器标识号。|  
|last_run_outcome|**tinyint**|作业上次运行的结果：<br /><br /> **0** = 失败<br /><br /> **1** = 成功<br /><br /> **3** = 取消|  
|last_outcome_ 消息|**nvarchar(1024)**|与 last_run_outcome 列关联的消息（如果有）。|  
|last_run_date|**int**|上次运行作业的日期。|  
|last_run_time|**int**|上次运行作业的时间。|  
|last_run_duration|**int**|作业运行的持续时间，以小时、分钟和秒为单位。 通过使用公式计算: (*小时*\*10000) + (*分钟*\*100) +*秒*。|  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理表&#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
