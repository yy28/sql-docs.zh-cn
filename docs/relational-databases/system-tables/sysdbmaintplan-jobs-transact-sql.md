---
title: sysdbmaintplan_jobs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_jobs
- sysdbmaintplan_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_jobs system table
ms.assetid: bc65cd70-6ef2-4c17-be11-877ecf4efe50
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e5797b84018e874021d828388d9b5af1f4237033
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889282"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中包含此表，以保留已从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本升级而来的实例的现有信息。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不更改此表的内容。 该表存储在**msdb**数据库中。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**job_id**|**uniqueidentifier**|与数据库维护计划关联的作业 ID。|  
  
  
