---
title: sysarticleupdates (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 384e6abd93369bd1913bddf31b8dec6f8541e0d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005574"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个支持即时更新订阅的项目在表中各占一行。 该表存储在复制的数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|为文章提供唯一的 ID 号标识列。|  
|**pubid**|**int**|项目所属发布的 ID。|  
|**sync_ins_proc**|**int**|处理插入同步事务的存储过程 ID。|  
|**sync_upd_proc**|**int**|处理更新同步事务的存储过程 ID。|  
|**sync_del_proc**|**int**|处理删除同步事务的存储过程 ID。|  
|**autogen**|**bit**|指示自动生成存储过程：<br /><br /> **0** = false，不自动。<br /><br /> **1** = true，自动。|  
|**sync_upd_trig**|**int**|项目表上自动版本控制触发器的 ID。|  
|**conflict_tableid**|**int**|冲突表的 ID。|  
|**ins_conflict_proc**|**int**|用于写入到冲突的过程的 ID **conflict_table**。|  
|**identity_support**|**bit**|指定使用排队更新时是否启用自动标识范围处理。 **0**意味着没有任何标识范围支持。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
