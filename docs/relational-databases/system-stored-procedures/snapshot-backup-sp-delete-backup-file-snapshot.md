---
title: sp_delete_backup_file_snapshot （Transact-sql） |Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 365ddae67f2357c11735f2d0966e56405edbde07
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053673"
---
# <a name="sp_delete_backup_file_snapshot-transact-sql"></a>sp_delete_backup_file_snapshot （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  从指定的数据库中删除指定的备份快照。 将此系统存储过程与**sys. fn_db_backup_file_snapshots** system 函数结合使用，以标识和删除孤立的备份快照。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N'<database_name>  
    , [ @snapshot_url = ] N'<snapshot_url>  
```  
  
## <a name="arguments"></a>自变量  
 *[ @db_name =] database_name*  
 包含要删除的快照的数据库的名称，以 Unicode 字符串形式提供。  
  
 *[ @snapshot_url =] snapshot_url*  
 要删除的快照的 URL，以 Unicode 字符串形式提供。  
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY DATABASE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sys. fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
