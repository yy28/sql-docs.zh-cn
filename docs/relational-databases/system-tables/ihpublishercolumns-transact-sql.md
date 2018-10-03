---
title: IHpublishercolumns (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6a8a2c4d6850b814d79b360ff9748579cf44b7b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757565"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumns**系统表表示发布服务器上存储的元数据。 此表的复制从非 SQL Server 发布服务器使用当前分发服务器的每个列对应一行。 数据类型中的信息**IHpublishercolumns**是特定于从中发布数据的非 SQL Server 数据库管理系统 (DBMS)。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|标识已发布列。|  
|**table_id**|**int**|标识从源表[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)列属于。|  
|**publisher_id**|**smallint**|标识非 SQL Server 发布服务器从其发布该列。|  
|**名称**|**sysname**|已发布列的名称。|  
|**column_ordinal**|**int**|按顺序标识列。|  
|**类型**|**varchar(255)**|发布服务器上源列的列数据类型。|  
|**长度**|**bigint**|发布服务器上源列的长度。|  
|**prec**|**int**|发布服务器上源列的精度。|  
|**scale**|**int**|发布服务器上源列的小数位数。|  
|**isnullable**|**bit**|指示列是否接受 NULL 值，其中**1**表示接受 NULL 值。|  
|**iscaptured**|**bit**|指示列上是否存在触发器，即使列没有在项目中发布，该列也可能存在。 值为**1**列存在该触发器的方式。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns&#40;系统视图&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
