---
title: MStracer_tokens (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 28c23c13147285f3569517a4afab79684dd6a99b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mstracertokens-transact-sql"></a>MStracer_tokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MStracer_tokens**表保留的跟踪令牌记录插入到发布的记录。 此表存储在分发数据库中，复制过程使用此表来监视性能。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|标识跟踪令牌记录。|  
|**publication_id**|**int**|标识跟踪令牌记录插入的发布。|  
|**publisher_commit**|**datetime**|在发布服务器提交跟踪令牌记录的日期和时间。|  
|**distributor_commit**|**datetime**|在分发服务器提交跟踪令牌记录的日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
