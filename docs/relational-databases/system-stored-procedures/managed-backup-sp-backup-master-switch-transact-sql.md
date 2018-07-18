---
title: managed_backup.sp_ backup_master_switch (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_ backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_ backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64d6681203962b54f1f3daae2de26e695cec240c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37995548"
---
# <a name="managedbackupsp-backupmasterswitch-transact-sql"></a>managed_backup.sp_ backup_master_switch (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  暂停或继续 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
 使用此存储过程可临时暂停然后继续 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 这样确保在操作继续进行时所有配置设置保持不变并得以保留。 暂停 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 时，不执行保持期。 这意味着不检查是否应从存储中删除文件，或是否有备份文件损坏或日志链中断。  
  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@state = ] { 0 | 1}  
```  
  
##  <a name="Arguments"></a> 参数  
 @state  
 设置 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的状态。 @state参数是**位**。 将其值设置为 0 时，操作暂停；将其值设置为 1 时，操作继续进行。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>Security  
 介绍与语句相关的安全问题。包括“权限”小节（H3 标题）。 在适当时考虑包括其他“所有权链接”和“审核”小节。  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**数据库角色的**ALTER ANY CREDENTIAL**权限，并且**EXECUTE**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="examples"></a>示例  
 可使用下例在执行 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的实例上暂停它：  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=0;  
Go  
  
```  
  
 可使用下例继续 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_master_switch @state=1;  
Go  
  
```  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Azure 的 SQL Server 托管备份](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
