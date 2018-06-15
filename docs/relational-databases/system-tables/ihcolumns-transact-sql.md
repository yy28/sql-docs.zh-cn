---
title: IHcolumns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d713dbd76921955aab6066b51d163a17ca7cba9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33001584"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHcolumns**系统表中包含每个已发布列对应的一行。 此表用于定义发布时，如何呈现列数据类型从非 SQL Server 发布服务器实质上是映射非 SQL Server 数据库管理系统 (DBMS) 之间的数据类型和 SQL Server。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|标识已发布列。|  
|**publishercolumn_id**|**int**|将已发布的列与列元数据存储在相关联[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系统表。|  
|**名称**|**sysname**|指定的列名称。|  
|**article_id**|**int**|标识列所属的项目。|  
|**column_ordinal**|**int**|按顺序标识列。|  
|**mapped_type**|**tinyint**|订阅服务器中目标列的列数据类型。|  
|**mapped_length**|**bigint**|订阅服务器中列的长度。|  
|**mapped_prec**|**int**|订阅服务器中列的精度。|  
|**mapped_scale**|**int**|订阅服务器中列的小数位数。|  
|**mapped_nullable**|**bit**|指示订阅服务器上的列是否接受 NULL 值，其中**1**意味着是否接受 NULL 值。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns&#40;系统视图&#41; &#40;Transact SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
