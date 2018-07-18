---
title: managed_backup.sp_backup_config_basic (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f8f6a2bb437982bdc40c70b9e53c6c864dbc5b4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984829"
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  配置[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]基本设置为特定数据库或实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  此过程可以调用在其自己创建基本的托管备份配置。 但是，如果你打算添加高级的功能或自定义计划，首先配置这些设置，请使用[managed_backup.sp_backup_config_advanced &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)并[managed_backup.sp_backup_config_schedule &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)启用托管的备份使用此过程之前。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> 参数  
 @enable_backup  
 启用或禁用指定数据库的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @enable_backup是**位**。 配置时所需的参数[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的第一个实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果要更改的现有[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置中，此参数是可选。 在这种情况下，未指定任何配置值保留其现有值。  
  
 @database_name  
 启用托管的备份上特定数据库的数据库名称。  
  
 @container_url  
 指示备份的位置的 URL。 当@credential_name为 NULL，此 URL 是指向 Azure 存储中的 blob 容器的共享的访问签名 (SAS) URL，并备份使用块 blob 功能的新备份。 有关详细信息，请查看[理解 SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。 当@credential_name指定，则这是存储帐户 URL，并将备份使用不推荐使用的备份到页 blob 功能。  
  
> [!NOTE]  
>  目前，如果此参数支持 SAS URL。  
  
 @retention_days  
 备份文件的保持期（以天为单位）。 @storage_url为 int。 配置时，这是一个必需的参数[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的实例上首次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 更改时[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置中，此参数是可选。 如果不指定，则会保留现有的配置值。  
  
 @credential_name  
 用于验证 Windows Azure 存储帐户身份的 SQL 凭据的名称。 @credentail_name 是**SYSNAME**。 指定时，备份存储到页 blob。 如果此参数为 NULL，则备份将存储为块 blob。 备份到页 blob 已弃用，因此应首选使用新的块 blob 备份功能。 当用于更改[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置时，此参数是可选参数。 如果未指定，会保留现有的配置值。  
  
> [!WARNING]  
>  **@credential_name**目前不支持参数。 支持仅备份到块 blob，这需要此参数为 NULL。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求的成员身份**db_backupoperator**数据库角色的**ALTER ANY CREDENTIAL**权限，并且**EXECUTE**权限**sp_delete_backuphistory**存储过程。  
  
## <a name="examples"></a>示例  
 可以使用最新的 Azure PowerShell 命令来创建存储帐户容器和 SAS URL。 下面的示例 mystorageaccount 的存储帐户中创建一个新容器，mycontainer，，然后为其获取 SAS URL，具有完全权限。  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 下面的示例启用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]为的 SQL Server，执行实例设置为 30 天的保留策略，将目标设置为一个名为 mycontainer 的存储帐户中名为 mystorageaccount 容器。  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 以下示例禁用在所在 SQL Server 实例上执行的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>请参阅  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
