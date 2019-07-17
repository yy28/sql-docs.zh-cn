---
title: backupmediafamily (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ea3fd7937447ba3ed0f3ad89965301dead772cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122884"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个介质簇在表中占一行。 如果介质簇驻留在镜像介质集中，则对于介质集中的每个镜像，该介质簇都具有一个单独的行。 此表存储中**msdb**数据库。  
    
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|标识该簇所属介质集的唯一标识号。 引用**backupmediaset （media_set_id)**|  
|**family_sequence_number**|**tinyint**|该介质簇在介质集中的位置。|  
|**media_family_id**|**uniqueidentifier**|标识介质簇的唯一标识号。 可以为 NULL。|  
|**media_count**|**int**|介质簇中的介质数。 可以为 NULL。|  
|**logical_device_name**|**nvarchar(128)**|在此备份设备的名称**sys.backup_devices.name**。 如果这是临时的备份设备 (而不是永久的备份设备中存在**sys.backup_devices**)，则**logical_device_name**为 NULL。|  
|**physical_device_name**|nvarchar(260) |备份设备的物理名称。 可以为 NULL。 备份和还原过程之间共享此字段。 它可能包含原始备份目标路径或原始还原源路径。 具体取决于是否备份或还原发生第一次为数据库服务器上。 请注意从同一个备份文件的连续还原在还原时将不更新而不考虑其位置的路径。 因此， **physical_device_name**字段不能用于查看所用的恢复路径。|  
|**device_type**|**tinyint**|备份设备的类型：<br /><br /> 2 = 磁盘<br /><br /> 5 = 磁带<br /><br /> 7 = 虚拟设备<br /><br /> 9 = azure 存储<br /><br /> 105 = 永久备份设备。<br /><br /> 可以为 NULL。<br /><br /> 中可以找到所有永久设备名称和设备号**sys.backup_devices**。|  
|**physical_block_size**|**int**|用于写入介质簇的物理块大小。 可以为 NULL。|  
|**mirror**|**tinyint**|镜像服务器号 (0-3)。|  
  
## <a name="remarks"></a>备注  
 RESTORE VERIFYONLY FROM*备份设备*WITH LOADHISTORY 使用的列来填充**backupmediaset**介质集标头中的相应值的表。  
  
 若要减少此表中和其他备份和历史记录表中的行数，请执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>请参阅  
 [备份和还原表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile (Transact-SQL)](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset (Transact-SQL)](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
