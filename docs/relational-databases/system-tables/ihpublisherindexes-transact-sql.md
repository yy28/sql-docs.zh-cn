---
title: IHpublisherindexes (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a24126ef3226878b4d07a056573f3b60e94495c3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802509"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherindexes**系统表中占一行复制从非 SQL Server 发布服务器使用当前分发服务器的每个索引。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|标识已发布的索引。|  
|**table_id**|**int**|标识从表[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)所属索引。|  
|**publisher_id**|**smallint**|标识非 SQL Server 发布服务器从中发布索引。|  
|**名称**|**sysname**|已发布的索引的名称。|  
|**类型**|**nvarchar(255)**|受支持的索引类型从[IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)系统表。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
