---
title: IHpublishercolumns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
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
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4bd15161e658348ea68c2f87c1468ede00bac5e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003754"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumns**系统表表示发布服务器上存储的元数据。 此表包含针对复制从非 SQL Server 发布服务器使用当前分发服务器的每个列提供一行。 数据类型中的信息**IHpublishercolumns**特定于非 SQL Server 数据库管理系统 (DBMS) 从其数据发布。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|标识已发布列。|  
|**table_id**|**int**|标识从源表[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)列所属。|  
|**publisher_id**|**int**|标识非 SQL Server 发布服务器从其发布的列。|  
|**名称**|**sysname**|已发布列的名称。|  
|**column_ordinal**|**int**|按顺序标识列。|  
|**类型**|**varchar(255)**|发布服务器上源列的列数据类型。|  
|**length**|**bigint**|发布服务器上源列的长度。|  
|**prec**|**int**|发布服务器上源列的精度。|  
|**小数位数**|**int**|发布服务器上源列的小数位数。|  
|**isnullable**|**bit**|指示列是否接受 NULL 值，其中**1**意味着是否接受 NULL 值。|  
|**iscaptured**|**bit**|指示列上是否存在触发器，即使列没有在项目中发布，该列也可能存在。 值为**1**意味着该触发器的列存在。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns&#40;系统视图&#41; &#40;Transact SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
