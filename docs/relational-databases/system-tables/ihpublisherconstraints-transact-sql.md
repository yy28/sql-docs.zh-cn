---
description: IHpublisherconstraints (Transact-SQL)
title: IHpublisherconstraints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 24ab58c617748d52c8c7463454b4d701bf826c42
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545744"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用当前分发服务器从非 SQL Server 发布服务器复制的每个约束在 **IHpublisherconstraints** 系统表中各占一行。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|标识所发布的约束。|  
|table_id****|**int**|标识约束所属的 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 中的表。|  
|**publisher_id**|**smallint**|标识正在发布该列的非 SQL Server 发布服务器。|  
|**名称**|**Sysname**|所发布的约束的名称。|  
|**类型**|**nvarchar(255)**|[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)系统表中受支持的约束类型。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
