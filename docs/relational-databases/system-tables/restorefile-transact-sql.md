---
title: restorefile (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffb5c6e1457a846bf211dfeb075f3270a7269736
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263040"
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个还原文件（包括按文件组名称间接还原的文件）在表中占一行。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|标识相应还原操作的唯一标识号。 引用**restorehistory(restore_history_id)**。|  
|**file_number**|**numeric(10,0)**|被还原文件的文件标识号。 每个数据库中的此标识号必须是唯一的。 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值的填充方式与完全还原时的填充方式相同。|  
|**destination_phys_drive**|nvarchar(260)|将文件还原到的驱动器或分区。 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值的填充方式与完全还原时的填充方式相同。|  
|**destination_phys_name**|nvarchar(260)|文件名，其中不含将文件还原到的驱动器或分区信息。 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值的填充方式与完全还原时的填充方式相同。|  
  
## <a name="remarks"></a>注释  
 若要减少在此表，其他备份和历史记录表中的行数，执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
