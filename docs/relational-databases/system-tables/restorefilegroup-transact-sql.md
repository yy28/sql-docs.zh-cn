---
title: "restorefilegroup (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- restorefilegroup_TSQL
- restorefilegroup
dev_langs: TSQL
helpviewer_keywords:
- filegroups [SQL Server], restorefilegroup system table
- restorefilegroup system table
ms.assetid: 3aa15c55-6b72-4f76-97d7-bd88391d105c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cbdf5074c50b2072ef60bdccb0541f4760bdd43
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restorefilegroup-transact-sql"></a>restorefilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个已还原的文件组在表中占一行。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|标识相应还原操作的唯一标识号。 引用**restorehistory(restore_history_id)**。|  
|**filegroup_name**|**nvarchar （128)**|被还原的文件组的名称 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值的填充方式与完全还原时的填充方式相同。|  
  
## <a name="remarks"></a>注释  
 若要减少在此表，其他备份和历史记录表中的行数，执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact SQL &#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorehistory &#40;Transact SQL &#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
