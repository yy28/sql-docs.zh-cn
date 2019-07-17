---
title: 值来生成 sysdbmaintplan_history (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4470b6b5d1b30f5698bf588a04066c50bb4c7197
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130452"
---
# <a name="sysdbmaintplanhistory-transact-sql"></a>sysdbmaintplan_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此表存储中**msdb**数据库。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**sequence_id**|**int**|数据库维护计划执行的历史记录序列。|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**plan_name**|**sysname**|数据库维护计划名称。|  
|**database_name**|**sysname**|与数据库维护计划关联的数据库的名称。|  
|**server_name**|**sysname**|系统名称。|  
|**活动**|**nvarchar(128)**|数据库维护计划执行的活动（例如备份事务日志等）。|  
|**succeeded**|**bit**|**0** = 成功**1** = 失败|  
|**end_time**|**datetime**|完成操作的时间。|  
|**duration**|**int**|完成数据库维护计划操作所需的时间。|  
|**start_time**|**datetime**|操作开始的时间。|  
|**error_number**|**int**|失败时报告的错误号。|  
|message |**nvarchar(512)**|生成的消息**sqlmaint**。|  
  
  
