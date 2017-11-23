---
title: "sp_replcounters (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords: sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3383f50142e04966a24515adcf08efbc4c5c60bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个发布数据库返回有关滞后时间、吞吐量和事务计数的复制统计信息。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**数据库**|**sysname**|数据库的名称。|  
|**复制的事务**|**int**|日志中等待传送到分发数据库的事务数。|  
|**复制速率 trans 数/秒**|**float**|平均每秒传送到分发数据库的事务数。|  
|**复制延迟**|**float**|事务在分发前位于日志中的平均时间（秒）。|  
|**Replbeginlsn**|**binary(10)**|日志中当前截断点的日志序列号 (LSN)。|  
|**Replendlsn**|**binary(10)**|等待传送到分发数据库的下一个提交记录的 LSN。|  
  
## <a name="remarks"></a>注释  
 **sp_replcounters**事务复制中使用。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**db_owner**固定的数据库角色或**sysadmin**固定的服务器角色。  
  
## <a name="see-also"></a>另请参阅  
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
