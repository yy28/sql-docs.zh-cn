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
author: stevestein
ms.author: sstein
ms.openlocfilehash: f780199361d9e5741187dd4e5346abb2df98b9cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130435"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中包含此表，以保留已从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本升级而来的实例的现有信息。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不更改此表的内容。 该表存储在**msdb**数据库中。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**job_id**|**uniqueidentifier**|与数据库维护计划关联的作业 ID。|  
  
  
