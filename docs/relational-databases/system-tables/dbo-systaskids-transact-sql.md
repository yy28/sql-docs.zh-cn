---
title: "dbo.systaskids (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20f08ae12092b6d5e0ffa33ad118cbd100a96338
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中创建的任务到当前版本中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 作业的映射。 此表存储在**msdb**数据库。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|任务 Id|  
|**job_id**|**uniqueidentifier**|任务所映射到的作业 ID|  
  
  
