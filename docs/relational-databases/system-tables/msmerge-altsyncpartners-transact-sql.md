---
title: MSmerge_altsyncpartners (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_altsyncpartners_TSQL
- MSmerge_altsyncpartners
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_altsyncpartners system table
ms.assetid: da51b0f8-5ad0-4aeb-96ed-2b3672a2a6e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7190c2a800ffcf71f9969725a9e43bd31ad0af9e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794289"
---
# <a name="msmergealtsyncpartners-transact-sql"></a>MSmerge_altsyncpartners (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_altsyncpartners**表跟踪发布服务器的当前同步伙伴是谁的关联。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|原始发布服务器的标识符。|  
|**alternate_subid**|**uniqueidentifier**|作为可选同步伙伴的订阅服务器的标识符。|  
|**description**|**nvarchar(255)**|对可选同步伙伴的说明。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
