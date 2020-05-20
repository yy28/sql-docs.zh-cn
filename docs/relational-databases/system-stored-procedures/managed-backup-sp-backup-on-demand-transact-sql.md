---
title: managed_backup sp_backup_on_demand （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bb2bda2d58504033469e8ed0f6455784efb113b8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830429"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup sp_backup_on_demand （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  请求 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 执行对指定数据库的备份。  
  
 使用此存储过程可对使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 配置的数据库执行即席备份。 这会阻止备份链中的任何中断， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 进程可感知，备份存储在同一个 Azure Blob 存储容器中。  
  
 成功完成备份后，将返回完整的备份文件路径。 其中包括备份操作中生成的新备份文件的名称和位置。  
  
 如果 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 正在对指定数据库执行给定类型的备份，则会返回一个错误。 在这种情况下，返回的错误消息包括当前备份将上载到的完整的备份文件路径。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>形参  
 @database_name  
 要对其执行备份的数据库的名称。 @database_name为**SYSNAME**。  
  
 @type  
 要执行的备份类型：数据库或日志。 @type参数为**NVARCHAR （32）**。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有**db_backupoperator**数据库角色的成员身份，具有**ALTER ANY CREDENTIAL**权限以及对**sp_delete_backuphistory**存储过程的**EXECUTE**权限。  
  
## <a name="examples"></a>示例  
 下面的示例为数据库 "TestDB" 创建数据库备份请求。 此数据库启用了 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 对于每个代码段，请在语言属性字段中选择“tsql”。  
  
  
