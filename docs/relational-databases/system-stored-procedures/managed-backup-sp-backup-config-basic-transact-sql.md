---
title: managed_backup. sp_backup_config_basic (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 92cbea99941b6e9378c4400ae0b563d462c34f27
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152036"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup. sp_backup_config_basic (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  为特定数据库或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例配置基本设置。[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
> [!NOTE]  
>  可以自行调用此过程来创建基本的托管备份配置。 但是, 如果计划添加高级功能或自定义计划, 请先使用 managed_backup 和 managed_backup 配置这些设置[。 &#40;&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) [sp_backup_config_schedule &#40;&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)在通过此过程启用托管备份之前的 transact-sql。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> 参数  
 @enable_backup  
 启用或禁用指定数据库的 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 @enable_backup是 **位**。 为的第一个[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例配置时所需的参数。 如果要更改现有[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置, 则此参数是可选的。 在这种情况下, 未指定的任何配置值都将保留其现有值。  
  
 @database_name  
 用于在特定数据库上启用托管备份的数据库名称。  
  
 @container_url  
 指示备份位置的 URL。 当@credential_name为 NULL 时, 此 URL 是 Azure 存储中 blob 容器的共享访问签名 (SAS) url, 备份使用新的备份来阻止 blob 功能。 有关详细信息, 请参阅[了解 SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)。 当@credential_name指定时, 这是一个存储帐户 URL, 备份使用不推荐使用的备份到页 blob 功能。  
  
> [!NOTE]  
>  目前此参数仅支持 SAS URL。  
  
 @retention_days  
 备份文件的保持期（以天为单位）。 @storage_url为 INT。 这是在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上首次[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置时所需的参数。 更改[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置时, 此参数是可选的。 如果不指定，则会保留现有的配置值。  
  
 @credential_name  
 用于对 Azure 存储帐户进行身份验证的 SQL 凭据的名称。 @credentail_name为**SYSNAME**。 指定时, 备份将存储到页 blob。 如果此参数为 NULL, 则备份将存储为块 blob。 备份到页 blob 已弃用, 因此最好使用新的块 blob 备份功能。 当用于更改[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]配置时，此参数是可选参数。 如果未指定, 则保留现有的配置值。  
  
> [!WARNING]
>  此 **@credential_name** 参数目前不受支持。 仅支持备份到块 blob, 这需要此参数为 NULL。  
  
## <a name="return-code-value"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 要求具有**db_backupoperator**数据库角色的成员身份, 具有**ALTER ANY CREDENTIAL**权限以及对**sp_delete_backuphistory**存储过程的**EXECUTE**权限。  
  
## <a name="examples"></a>示例  
 可以使用最新的 Azure PowerShell 命令创建存储帐户容器和 SAS URL。 以下示例在 mystorageaccount 存储帐户中创建一个新容器 mycontainer, 然后获取具有完全权限的 SAS URL。  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 下面的示例[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]在中执行 SQL Server 的实例, 将保留策略设置为30天, 将目标设置为名为 "mystorageaccount" 的存储帐户中名为 "mycontainer" 的容器。  
  
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
  
  
