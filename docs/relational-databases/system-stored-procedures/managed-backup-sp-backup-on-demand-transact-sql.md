---
title: managed_backup.sp_backup_on_demand (TRANSACT-SQL) |Microsoft Docs
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
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d95bdd7fa337598c289aaa7a958c33513eec12d0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38058035"
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  请求 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 执行对指定数据库的备份。  
  
 使用此存储过程可对使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 配置的数据库执行即席备份。 这样做可以防止备份链中出现任何中断，[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 过程可识别并且备份存储在同一 Windows Azure Blob 存储容器中。  
  
 成功完成备份后，将返回完整的备份文件路径。 其中包括备份操作中生成的新备份文件的名称和位置。  
  
 如果 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 正在对指定数据库执行给定类型的备份，则会返回一个错误。 在这种情况下，返回的错误消息包括当前备份将上载到的完整的备份文件路径。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 参数  
 @database_name  
 要对其执行备份的数据库的名称。 @database_name是**SYSNAME**。  
  
 @type  
 要执行的备份类型：数据库或日志。 @type参数是**nvarchar （32)**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**数据库角色的**ALTER ANY CREDENTIAL**权限，并且**EXECUTE**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="examples"></a>示例  
 以下示例发出了对数据库“TestDB”的数据库备份请求。 此数据库启用了 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 对于每个代码段，请在语言属性字段中选择“tsql”。  
  
  
