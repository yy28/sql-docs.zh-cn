---
title: "backupmediafamily (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b2435ce3fe98104aaf3bbb857e89779adb221e4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个介质簇在表中占一行。 如果介质簇驻留在镜像介质集中，则对于介质集中的每个镜像，该介质簇都具有一个单独的行。 此表存储在**msdb**数据库。  
    
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|标识该簇所属介质集的唯一标识号。 References **backupmediaset(media_set_id)**|  
|**family_sequence_number**|**tinyint**|该介质簇在介质集中的位置。|  
|**media_family_id**|**uniqueidentifier**|标识介质簇的唯一标识号。 可以为 NULL。|  
|**media_count**|**int**|介质簇中的介质数。 可以为 NULL。|  
|**logical_device_name**|**nvarchar(128)**|在此备份设备的名称**sys.backup_devices.name**。 如果这是临时的备份设备 (而不是永久的备份设备中存在**sys.backup_devices**) 的值**logical_device_name**为 NULL。|  
|**physical_device_name**|nvarchar(260)|备份设备的物理名称。 可以为 NULL。|  
|**device_type**|**tinyint**|备份设备的类型：<br /><br /> 2 = 磁盘<br /><br /> 5 = 磁带<br /><br /> 7 = 虚拟设备<br /><br /> 105 = 永久备份设备。<br /><br /> 可以为 NULL。<br /><br /> 中可以找到所有永久设备的名称和设备号**sys.backup_devices**。|  
|**physical_block_size**|**int**|用于写入介质簇的物理块大小。 可以为 NULL。|  
|**mirror**|**tinyint**|镜像服务器号 (0-3)。|  
  
## <a name="remarks"></a>注释  
 RESTORE VERIFYONLY 从*backup_device*与 LOADHISTORY 填充的列**backupmediaset**介质集标头中的相应值的表。  
  
 若要减少在此表，其他备份和历史记录表中的行数，执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile (Transact-SQL)](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset (Transact-SQL)](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系统表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
