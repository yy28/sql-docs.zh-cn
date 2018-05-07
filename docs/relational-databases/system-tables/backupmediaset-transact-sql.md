---
title: backupmediaset (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21e327f7c630b106a52a0bd720cbf94f8b4a23fd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个备份介质集在表中占一行。 此表存储在**msdb**数据库。  
 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|唯一介质集标识号。 标识，主键。|  
|**media_uuid**|**uniqueidentifier**|介质集的 UUID。 所有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]媒体集具有 UUID。<br /><br /> 对于早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但是，如果介质集包含仅一个介质簇**media_uuid**列可能为 NULL (**media_family_count**为 1)。|  
|**media_family_count**|**tinyint**|媒体集中的媒体簇数。 可以为 NULL。|  
|**名称**|**nvarchar(128)**|介质集的名称。 可以为 NULL。<br /><br /> 有关详细信息，请参阅 MEDIANAME 和 MEDIADESCRIPTION 中的[备份&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。|  
|**说明**|**nvarchar(255)**|介质集的文本化说明。 可以为 NULL。<br /><br /> 有关详细信息，请参阅 MEDIANAME 和 MEDIADESCRIPTION 中的[备份&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。|  
|**software_name**|**nvarchar(128)**|写入介质标签的备份软件名称。 可以为 NULL。|  
|**software_vendor_id**|**int**|写入备份介质标签的软件供应商标识号。 可以为 NULL。<br /><br /> 值[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是十六进制 0x1200。|  
|**MTF_major_version**|**tinyint**|用于生成该介质集的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 磁带格式的主要版本号。 可以为 NULL。|  
|**mirror_count**|**tinyint**|介质集中的镜像数。|  
|**is_password_protected**|**bit**|指定介质集是否受到密码保护：<br /><br /> 0 = 未受到保护<br /><br /> 1 = 受到保护|  
|**is_compressed**|**bit**|备份是否已压缩：<br /><br /> 0 = 未压缩<br /><br /> 1 = 压缩<br /><br /> 期间**msdb**升级，此值设置为 NULL。 表示未压缩的备份。|  
|**is_encrypted**|**Bit**|备份是否已加密：<br /><br /> 0 = 未加密<br /><br /> 1 = 已加密|  
  
## <a name="remarks"></a>注释  
 RESTORE VERIFYONLY 从*backup_device*与 LOADHISTORY 填充的列**backupmediaset**介质集标头中的相应值的表。  
  
 若要减少在此表，其他备份和历史记录表中的行数，执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile (Transact-SQL)](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup (Transact-SQL)](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily (Transact-SQL)](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
