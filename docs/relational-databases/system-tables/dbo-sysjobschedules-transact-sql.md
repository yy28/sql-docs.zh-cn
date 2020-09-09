---
description: dbo.sysjobschedules (Transact-SQL)
title: dbo.sysjobschedules (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2cd3180f982b978a5918b505f9cf0989baf4e0fa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544583"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含将由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的作业的计划信息。 该表存储在 **msdb** 数据库中。  
  
> **注意：****Sysjobschedules**表每20分钟刷新一次，这可能会影响**sp_help_jobschedule**存储过程返回的值。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|计划的 ID。|  
|**job_id**|**uniqueidentifier**|作业的 ID。|  
|**next_run_date**|**int**|计划运行作业的下一个日期。 日期格式为 YYYYMMDD。|  
|**next_run_time**|**int**|计划运行作业的时间。 此时间的格式为 HHMMSS，并使用24小时制。|  
  
## <a name="see-also"></a>另请参阅  
 [dbo.sys计划 &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
