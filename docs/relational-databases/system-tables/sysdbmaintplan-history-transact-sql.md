---
title: sysdbmaintplan_history （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_history_TSQL
- sysdbmaintplan_history
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_history system table
ms.assetid: 02d36f08-ac93-4463-bb59-284c5cd6ed04
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ec49500e94a22e8ab91513fa9436cd6d21bf7959
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881419"
---
# <a name="sysdbmaintplan_history-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  该表存储在**msdb**数据库中。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|数据库维护计划执行的历史记录序列。|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**plan_name**|**sysname**|数据库维护计划名称。|  
|**database_name**|**sysname**|与数据库维护计划关联的数据库的名称。|  
|server_name|**sysname**|系统名称。|  
|**activity**|**nvarchar(128)**|数据库维护计划执行的活动（例如备份事务日志等）。|  
|**成功**|**bit**|**0** = 成功**1** = 失败|  
|**end_time**|**datetime**|完成操作的时间。|  
|**duration**|**int**|完成数据库维护计划操作所需的时间。|  
|**start_time**|**datetime**|操作开始的时间。|  
|error_number |**int**|失败时报告的错误号。|  
|**message**|**nvarchar(512)**|**Sqlmaint**生成的消息。|  
  
  
