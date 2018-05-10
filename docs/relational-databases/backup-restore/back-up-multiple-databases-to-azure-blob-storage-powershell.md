---
title: 将多个数据库备份到 Azure Blob 存储 - PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: babe7c958f6832dc3e77c4718595e4c6967fe566
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>将多个数据库备份到 Azure Blob 存储 - PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题提供一些示例脚本，可用于通过 PowerShell cmdlet 自动备份到 Windows Azure Blob 存储服务。  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>用于备份和还原的 PowerShell cmdlet 的概述  
 **Backup-SqlDatabase** 和 **Restore-SqlDatabase** 是两个用于进行备份和还原操作的主要 cmdlet。 此外，可能还需要其他 cmdlet 才能自动备份到 Windows Azure Blob 存储，如这组 **SqlCredential** cmdlet。下面列出了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中提供的用于备份和还原操作中的 PowerShell cmdlet。  
  
 Backup-SqlDatabase  
 此 cmdlet 用于创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份。  
  
 Restore-SqlDatabase  
 用于还原数据库。  
  
 New-SqlCredential  
 此 cmdlet 用于创建一个 SQL 凭据，后者用于 SQL Server 备份到 Windows Azure 存储。 有关凭据及其在 SQL Server 备份和还原中的使用情况的详细信息，请参阅 [使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 Get-SqlCredential  
 此 cmdlet 用于检索凭据对象及其属性。  
  
 Remove-SqlCredential  
 删除 SQL 凭据对象。  
  
 Set-SqlCredential  
 此 cmdlet 用于更改或设置 SQL 凭据对象的属性。  
  
> [!TIP]  
>  凭据 cmdlet 用于备份和还原到 Windows Azure Blob 存储的场景中。  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>用于多数据库、多实例备份操作的 PowerShell  
 以下几个部分包含用于多种操作的脚本，如在多个 SQL Server 实例上创建 SQL 凭据，备份 SQL Server 实例中的所有用户数据库等。 可使用这些脚本根据所处环境的要求自动进行备份操作或安排备份操作。 此处提供的脚本仅为示例，可针对所处环境修改或扩展这些脚本。  
  
 以下是这些示例脚本的注意事项：  
  
1.  **在 SQL Server PowerShell 路径中导航：** Windows PowerShell 实现了一些 cmdlet，可在表示 PowerShell 提供程序支持的对象层次的路径结构中导航。 在您导航到该路径中的节点时，可以使用其他 cmdlet 以便针对当前对象执行基本操作。  
  
2.  **Get-ChildItem** cmdlet： **Get-ChildItem** 返回的信息取决于 SQL Server PowerShell 路径中的位置。 例如，如果该位置在计算机级别，则此 cmdlet 返回计算机上安装的所有 SQL Server 数据库引擎实例。 再举一个例子，如果该位置在数据库等对象级别，则此 cmdlet 返回数据库对象的列表。  默认情况下， **Get-ChildItem** cmdlet 不返回系统对象。  使用 -Force 参数可查看系统对象。  
  
     有关详细信息，请参阅 [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md)。  
  
3.  尽管可通过更改变量值独立尝试每个代码示例，但对于所有备份和还原到 Windows Azure Blob 存储服务的操作，创建 Windows Azure 存储帐户和 SQL 凭据均为先决条件和必备条件。  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>在所有 SQL Server 实例上创建 SQL 凭据  
 下面有两个示例脚本，并且二者都在计算机上的所有 SQL Server 实例上创建 SQL 凭据“mybackupToURL”。 第一个示例比较简单，它创建凭据但不捕获异常。  例如，如果计算机的某个实例上已有同名的现有凭据，则该脚本将失败。 第二个示例捕获错误并允许脚本继续运行。  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | new-sqlcredential -Name $credentialName  -Identity $storageAccount -Secret $secureString  
```  
  
```  
  
import-module sqlps  
  
# set the parameter values  
  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#loop through instances and create a SQL credential, output any errors  
foreach ($instance in $instances)  
{  
    Try  
{  
     new-sqlcredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop   
}  
Catch [Exception]  
    {  
  
            write-host "instance - $($instance.name): "$_.Exception.Message  
  
    }  
  
 }  
  
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>从所有 SQL Server 实例中删除 SQL 凭据  
 此脚本可用于从计算机上安装的所有 SQL Server 实例中删除某个特定凭据。 如果某个特定实例上不存在凭据对象，则显示一条错误消息，而该脚本继续运行，直到检查完所有实例。  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-childitem  
  
foreach ($instance in $instances)  
   {   
    try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-sqlCredential -path $path -ea stop   
         }  
         catch [Exception]  
         {  
            write-host $_.Exception.Message  
  
        }  
  
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>为所有数据库（包括系统数据库）进行完整数据库备份  
 以下脚本创建计算机上所有数据库的备份。 其中包括用户数据库和 **msdb** 系统数据库。 该脚本筛选出 **tempdb** 和 **model** 系统数据库。  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>为所有用户数据库进行完整数据库备份  
 以下脚本可用于备份计算机上所有 SQL Server 实例上的所有用户数据库。  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>为所有 SQL Server 实例上的 MASTER 和 MSDB（系统数据库）进行完整数据库备份  
 以下脚本可用于备份在计算机上安装的所有 SQL Server 实例上的 **master** 和 **msdb** 数据库。  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>为 SQL Server 实例上的所有用户数据库进行完整数据库备份  
 以下脚本用于仅备份具名的 SQL Server 实例上提供的用户数据库。 更改 $srvPath 参数值后，同一脚本还可用于计算机上的默认实例。  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>仅为 SQL Server 实例上的系统数据库（MASTER 和 MSDB）进行完整数据库备份  
 完整脚本可用于备份 SQL Server 的命名实例上的 **master** 和 **msdb** 数据库。 更改 $srvPath 参数值后，同一脚本还可用于计算机上的默认实例。  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 Microsoft Azure Blob 存储服务进行 SQL Server 备份和还原](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server 备份到 URL 最佳实践和故障排除](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
