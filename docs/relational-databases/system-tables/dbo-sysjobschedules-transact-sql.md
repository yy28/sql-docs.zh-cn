---
title: dbo. sysjobschedules （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
author: stevestein
ms.author: sstein
ms.openlocfilehash: a7f2dfc6196bfba6c274eb45a45745159447cc39
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68061182"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含将由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的作业的计划信息。 该表存储在**msdb**数据库中。  
  
> **注意：****Sysjobschedules**表每20分钟刷新一次，这可能会影响**sp_help_jobschedule**存储过程返回的值。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|计划的 ID。|  
|**job_id**|**uniqueidentifier**|作业的 ID。|  
|**next_run_date**|**int**|计划运行作业的下一个日期。 日期格式为 YYYYMMDD。|  
|**next_run_time**|**int**|计划运行作业的时间。 此时间的格式为 HHMMSS，并使用24小时制。|  
  
## <a name="see-also"></a>另请参阅  
 [sysschedules 引用 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
