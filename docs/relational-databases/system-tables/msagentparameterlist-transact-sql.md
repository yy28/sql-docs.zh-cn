---
title: MSagentparameterlist (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bdbba583ece9a4a9020b27803ac07cf12137f1c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagentparameterlist**表包含复制代理参数信息，用于指定可以为给定的代理类型设置的参数。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|代理的类型：<br /><br /> **1** = 快照代理。<br /><br /> **2** = 日志读取器代理。<br /><br /> **3** = 分发代理。<br /><br /> **4** = 合并代理。<br /><br /> **9** = 队列读取器代理。|  
|**parameter_name**|**sysname**|有效代理参数的名称。|  
|**default_value**|**nvarchar(4000)**|代理参数的默认值，在这里，NULL 指示不存在这样的值。|  
|**min_value**|**int**|设置代理参数的下限，在这里，NULL 指示没有下限。|  
|**max_value**|**int**|设置代理参数的上限，在这里，NULL 指示没有上限。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
