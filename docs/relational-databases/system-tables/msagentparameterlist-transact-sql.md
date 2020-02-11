---
title: Msdb.dbo.msagentparameterlist （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: stevestein
ms.author: sstein
ms.openlocfilehash: d0ba22c75e36cc927fbd923af25aad48b3d02801
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68119250"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Msdb.dbo.msagentparameterlist**表包含复制代理参数信息，用于指定可为给定代理类型设置的参数。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|代理的类型：<br /><br /> **1** = 快照代理。<br /><br /> **2** = 日志读取器代理。<br /><br /> **3** = 分发代理。<br /><br /> **4** = 合并代理。<br /><br /> **9** = 队列读取器代理。|  
|**parameter_name**|**sysname**|有效代理参数的名称。|  
|**default_value**|**nvarchar(4000)**|代理参数的默认值，在这里，NULL 指示不存在这样的值。|  
|**min_value**|**int**|设置代理参数的下限，在这里，NULL 指示没有下限。|  
|**max_value**|**int**|设置代理参数的上限，在这里，NULL 指示没有上限。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
