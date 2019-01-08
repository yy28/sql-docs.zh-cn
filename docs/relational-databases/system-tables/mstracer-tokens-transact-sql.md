---
title: MStracer_tokens (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MStracer_tokens_TSQL
- MStracer_tokens
dev_langs:
- TSQL
helpviewer_keywords:
- MStracer_tokens system table
ms.assetid: b273aa48-8188-4213-8e2c-311543c3236f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 544bf835aaeda98b24169899eb5adfaae4e003e5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822891"
---
# <a name="mstracertokens-transact-sql"></a>MStracer_tokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MStracer_tokens**表维护插入发布的跟踪令牌记录的记录。 此表存储在分发数据库中，复制过程使用此表来监视性能。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|标识跟踪令牌记录。|  
|**publication_id**|**int**|标识跟踪令牌记录插入的发布。|  
|**publisher_commit**|**datetime**|在发布服务器提交跟踪令牌记录的日期和时间。|  
|**distributor_commit**|**datetime**|在分发服务器提交跟踪令牌记录的日期和时间。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
