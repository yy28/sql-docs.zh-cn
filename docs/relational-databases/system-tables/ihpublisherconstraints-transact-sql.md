---
title: IHpublisherconstraints (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d924e432a45d900092be6e84ed110afd66951d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732525"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherconstraints**系统表中占一行复制从非 SQL Server 发布服务器使用当前分发服务器的每个约束。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|标识所发布的约束。|  
|**table_id**|**int**|标识从表[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)约束所属。|  
|**publisher_id**|**smallint**|标识非 SQL Server 发布服务器从其发布该列。|  
|**名称**|**sysname**|所发布的约束的名称。|  
|**类型**|**nvarchar(255)**|受支持的约束类型从[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)系统表。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
