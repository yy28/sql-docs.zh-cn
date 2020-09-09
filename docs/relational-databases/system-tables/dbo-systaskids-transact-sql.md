---
description: dbo.systaskids (Transact-SQL)
title: dbo.systaskids (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3a3e639fcc99f3b78d499e76062cd7f6d32f516c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551054"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本中创建的任务到当前版本中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 作业的映射。 该表存储在 **msdb** 数据库中。  
  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|任务 Id|  
|**job_id**|**uniqueidentifier**|任务所映射到的作业 ID|  
  
  
