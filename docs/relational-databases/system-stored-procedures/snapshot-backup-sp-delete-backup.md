---
title: sp_delete_backup (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4125fa3a9a3a836b7cc710f58db0563b74eb8357
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  删除所有快照和构成快照备份集从指定的数据库的备份文件。 此系统存储过程是用于管理快照备份集的唯一推荐的方法。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>参数  
 *[ @backup_url = ] backup_meta_file_url*  
 要删除，从而会删除包含指定的备份集包括备份文件本身的所有快照的备份的 URL。  
  
 *[ @db_name =] database_name*  
 包含要删除的快照的数据库名称。 数据库名称时提供，系统会验证备份 URL 提供是指定的数据库的备份 URL，并使用[sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) ，删除每个快照。 如果未不提供任何数据库名称，则不会执行此数据库检查。  
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY DATABASE 权限或对指定的数据库的 ALTER 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys.fn_db_backup_file_snapshots &#40;Transact SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
