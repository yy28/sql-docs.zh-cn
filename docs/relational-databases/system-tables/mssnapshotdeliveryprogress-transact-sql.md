---
title: MSsnapshotdeliveryprogress (Transact SQL) |Microsoft 文档
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
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e0167319af3e6477cf5da2645ec7d8ee912f3646
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshotdeliveryprogress**表用于跟踪已成功传递到订阅服务器在应用快照时的文件。 此数据用于在合并代理无法在会话时传送所有文件的情况下恢复文件传送，从而避免在下次运行合并代理时传送相同文件。 此表存储在订阅服务器的订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|nvarchar(260)|标识从中成功传送文件的快照文件夹的路径。 对于使用参数化筛选器，该字符串的发布**dynsnap**将附加到值。|  
|**progress_token_hash**|**int**|生成的哈希值的值基于*progress_token*使用提高查找效率的给定*progress_token*值。|  
|**progress_token**|**nvarchar(500)**|标识已成功传送的文件，其值为文件名和路径的组合。|  
|**progress_timestamp**|**datetime**|**Datetime**值，该值指示成功传递快照文件。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
