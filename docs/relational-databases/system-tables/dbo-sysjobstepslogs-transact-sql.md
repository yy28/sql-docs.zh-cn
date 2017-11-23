---
title: "dbo.sysjobstepslogs (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs: TSQL
helpviewer_keywords: sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 050feecde1f82ca8962552744e2fc2d43d28bd4c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤的作业步骤日志，这些作业步骤配置为将作业步骤输出写入表中。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|作业步骤日志的 ID。|  
|**日志**|**nvarchar(max)**|作业步骤日志内容。|  
|**date_created**|**datetime**|创建作业步骤日志的日期和时间。|  
|**date_modified**|**datetime**|上次修改作业步骤日志的日期和时间。|  
|**log_size**|**int**|作业步骤日志的大小（以字节为单位）。|  
|**step_uid**|**uniqueidentifier**|作业步骤的唯一标识符。|  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_jobsteplog &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
