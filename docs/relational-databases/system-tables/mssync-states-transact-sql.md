---
title: MSsync_states （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsync_states
- MSsync_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsync_states system table
ms.assetid: b25e17e1-7718-432e-a442-c4946741d474
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bc81e41299041b50e53074cd4a133c6bd9c0cf9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016508"
---
# <a name="mssync_states-transact-sql"></a>MSsync_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsync_states**表将跟踪哪个发布仍处于并发快照模式。 此表存储在分发数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|发布服务器 ID。|  
|**publisher_db**|**sysname**|发布数据库的名称。|  
|**publication_id**|**int**|发布 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的 Integration Services 表](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;备份和还原表](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [日志传送表 (Transact-SQL)](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
