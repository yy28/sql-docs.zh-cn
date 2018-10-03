---
title: sysdbmaintplan_jobs (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0e54355cf0c7806c70f6bb80ee0463744b4c869b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794934"
---
# <a name="sysdbmaintplanjobs-transact-sql"></a>sysdbmaintplan_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中包含此表，以保留已从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本升级而来的实例的现有信息。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不更改此表的内容。 此表存储中**msdb**数据库。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**job_id**|**uniqueidentifier**|与数据库维护计划关联的作业 ID。|  
  
  
