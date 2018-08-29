---
title: sp_delete_backup_file_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd88ab54a8ab87be0601565c73e4e84a87790357
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032786"
---
# <a name="spdeletebackupfilesnapshot-transact-sql"></a>sp_delete_backup_file_snapshot (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  从指定的数据库中删除指定的备份快照。 使用此系统存储过程结合**sys.fn_db_backup_file_snapshots**系统函数来标识和删除孤立的备份快照。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N’<database_name>  
    , [ @snapshot_url = ] N’<snapshot_url>  
```  
  
## <a name="arguments"></a>参数  
 *[ @db_name =] 数据库名称*  
 包含要删除，作为 Unicode 字符串提供的快照的数据库的名称。  
  
 *[ @snapshot_url = ] snapshot_url*  
 若要删除，作为 Unicode 字符串提供快照的 URL。  
  
## <a name="permissions"></a>Permissions  
 要求具有 ALTER ANY DATABASE 权限。  
  
## <a name="see-also"></a>请参阅  
 [sys.fn_db_backup_file_snapshots &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
