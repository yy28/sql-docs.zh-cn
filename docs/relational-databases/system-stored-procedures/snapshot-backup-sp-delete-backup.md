---
title: sp_delete_backup （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67941825"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  从指定数据库中删除构成快照备份集的所有快照和备份文件。 仅建议使用此系统存储过程来管理快照备份集。 有关详细信息，请参阅[Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>参数  
 *[ @backup_url =] backup_meta_file_url*  
 要删除的备份的 URL，该 URL 将删除由指定的备份集组成的所有快照，包括备份文件本身。  
  
 *[ @db_name =] database_name*  
 包含要删除的快照的数据库的名称。 如果提供了数据库名称，系统将验证提供的备份 URL 是否为指定数据库的备份 URL，并使用[sp_delete_backup_file_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)删除每个快照。 如果未提供任何数据库名称，则不会执行此数据库检查。  
  
## <a name="permissions"></a>权限  
 需要对指定的数据库具有 ALTER ANY DATABASE 权限或 ALTER 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys. fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
