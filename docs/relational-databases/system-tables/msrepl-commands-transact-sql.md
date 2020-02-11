---
title: MSrepl_commands （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_commands
- MSrepl_commands_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_commands system table
ms.assetid: 53b9f9cd-9429-47a0-aba2-908fc60e7036
author: stevestein
ms.author: sstein
ms.openlocfilehash: c02a0201483617966d7d1c8aadfbad4ab39971e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127433"
---
# <a name="msrepl_commands-transact-sql"></a>MSrepl_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_commands**表包含复制的命令行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID。|  
|**xact_seqno**|**varbinary （16）**|事务序列号。|  
|type |**int**|命令类型。|  
|**article_id**|**int**|项目的 ID。|  
|**originator_id**|**int**|发起方的 ID。|  
|**command_id**|**int**|命令的 ID。|  
|**partial_command**|**bit**|指示这是否为部分命令。|  
|**command**|**varbinary （1024）**|命令值。|  
|**hashkey**|**int**|仅供内部使用。|  
|**originator_lsn**|**varbinary （16）**|标识原始发布中命令的 LSN。 这在对等事务复制中使用。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replcmds (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)  
  
  
