---
title: RESTORE DATABASE（并行数据仓库）| Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0fb3c753e4bde29eb9b5cbb5f287fc18d03a117a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782428"
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE（并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  将[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]用户数据库从数据库备份还原到[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备。 数据库会从以前通过[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [BACKUP DATABASE（并行数据仓库）](../../t-sql/statements/backup-database-parallel-data-warehouse.md)命令创建的备份进行还原。 使用备份和还原操作生成灾难恢复计划，或将数据库从一个设备移动到另一个。  
  
> [!NOTE]  
>  还原 master 包括还原设备登录信息。 若要还原 master，请使用 **Configuration Manager** 工具中的[还原 master 数据库 (Transact-SQL)](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) 页面。 有权访问控制节点的管理员可以执行此操作。  
  
 有关[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库备份的详细信息，请参阅[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的“备份和还原”。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>参数  
 RESTORE DATABASE database_name  
 指定要将用户数据库还原到名为 database_name 的数据库。 还原的数据库可以具有与备份的源数据库不同的名称。 database_name 不能作为数据库已存在于目标设备上。 有关允许的数据库名称的详细信息，请参阅[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的“对象命名规则”。  
  
 还原用户数据库会还原完整数据库备份，然后可以选择将差异备份还原到设备。 用户数据库的还原包括还原数据库用户和数据库角色。  
  
 FROM DISK = '\\\\UNC_path\\backup_directory'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将从中还原备份文件的网络路径和目录。 例如，FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'。  
  
 *backup_directory*  
 指定包含完整或差异备份的目录的名称。 例如，可以对完整或差异备份执行 RESTORE HEADERONLY 操作。  
  
 *full_backup_directory*  
 指定包含完整备份的目录的名称。  
  
 *differential_backup_directory*  
 指定包含差异备份的目录的名称。  
  
-   路径和备份目录必须已存在，并且必须指定为完全限定的通用命名约定 (UNC) 路径。  
  
-   备份目录的路径不能是本地路径，并且不能是任何[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备节点上的位置。  
  
-   UNC 路径和备份目录名称的最大长度为 200 个字符。  
  
-   必须以 IP 地址的形式指定服务器或主机。  
  
 RESTORE HEADERONLY  
 指定仅返回一个用户数据库备份的标头信息。 在其他字段中，标头包括备份的文本说明和备份名称。 备份名称无需与用于存储备份文的目录的名称相同。  
  
 RESTORE HEADERONLY 结果会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 结果之后模式化。 结果具有 50 多列，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 并不使用所有这些列。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY 结果中的列的说明，请参阅 [RESTORE HEADERONLY (Transact-SQL)](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 需要 **CREATE ANY DATABASE** 权限。  
  
 需要有权访问和读取备份目录的 Windows 帐户。 还必须将 Windows 帐户名称和密码存储在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中。  
  
1.  若要验证凭据是否已存在，请使用 [sys.dm_pdw_network_credentials (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)。  
  
2.  若要添加或更新凭据，请使用 [sp_pdw_add_network_credentials（SQL 数据仓库）](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)。  
  
3.  若要从[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中删除凭据，请使用 [sp_pdw_remove_network_credentials（SQL 数据仓库）](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)。  
  
## <a name="error-handling"></a>错误处理  
 RESTORE DATABASE 命令会在以下情况下导致错误：  
  
-   要还原的数据库的名称已在目标设备上存在。 若要避免此问题，请选择唯一的数据库名称，或在运行还原之前删除现有数据库。  
  
-   备份目录中存在一组无效的备份文件。  
  
-   登录权限不足以还原数据库。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]对备份文件所处的网络位置不拥有正确权限。  
  
-   备份目录的网络位置不存在或不可用。  
  
-   计算节点或控制节点上的磁盘空间不足。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不会在启动还原之前确认设备上是否存在足够磁盘空间。 因此，运行 RESTORE DATABASE 语句时可能会生成磁盘空间不足错误。 磁盘空间不足时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会回滚还原。  
  
-   数据库还原到的目标设备的计算节点比从中备份数据库的源设备更少。  
  
-   从事务中尝试进行数据库还原。  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会跟踪数据库还原是否成功。 还原差异数据库备份之前，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会验证完整数据库还原是否已成功完成。  
  
 还原之后，用户数据库会具有数据库兼容级别 120。 这适用于所有数据库（与其原始兼容级别无关）。  
  
 **还原到计算节点数更大的设备**  
在将数据库从较小设备还原到较大设备之后运行 [DBCC SHRINKLOG（Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)，因为重新分发会增加事务日志。  

将备份还原到计算节点数更大的设备会与计算节点数成比例地增加分配的数据库大小。  
  
例如，将 60 GB 数据库从 2 节点设备（每个节点 30 GB）还原到 6 节点设备时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会在 6 节点设备上创建 180 GB 数据库（6 个节点，每个节点 30 GB）。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]最初将数据库还原到 2 个节点以匹配源配置，然后将数据重新分发到所有 6 个节点。  
  
 重新分发之后，与较小源设备上的每个计算节点相比，每个计算节点都会包含较少的实际数据和较多的可用空间。 使用附加空间可将更多数据添加到数据库。 如果还原的数据库大小大于所需大小，则可以使用 [ALTER DATABASE（并行数据仓库）](../../t-sql/statements/alter-database-transact-sql.md?&tabs=sqlpdw)收缩数据库文件大小。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 对于这些限制和局限，源设备是从中创建数据库备份的设备，而目标设备是将数据库还原到的设备。  
  
 还原数据库不会自动重新生成统计信息。  
  
 在任何给定时间，只有一个 RESTORE DATABASE 或 BACKUP DATABASE 语句可以在设备上运行。 如果同时提交多个备份和还原语句，则设备会将它们放入队列中，一次处理一个。  
  
 只能将数据库备份还原到计算节点数等于或多于源设备的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目标设备。 目标设备的计算节点数不能少于源设备。  
  
 无法将在具有 SQL Server 2012 PDW 硬件的设备上创建的备份还原到具有 SQL Server 2008 R2 硬件的设备。 即使设备在最初购买时具有 SQL Server 2008 R2 PDW 硬件，而现在正在运行 SQL Server 2012 PDW 软件，情况也是如此。  
  
## <a name="locking"></a>锁定  
 在 DATABASE 对象上采用排他锁。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-restore-examples"></a>A. 简单 RESTORE 示例  
 下面的示例将完整备份还原到 `SalesInvoices2013` 数据库。 备份文件存储在 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 目录中。 SalesInvoices2013 数据库不能已在目标设备上存在，否则此命令会失败并出错。  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. 还原完整和差异备份  
 下面的示例将完整备份，然后将差异备份还原到 SalesInvoices2013 数据库  
  
 数据库的完整备份从存储在“\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full”目录中的完整备份还原。 如果还原成功完成，则差异备份会还原到 SalesInvoices2013 数据库。  差异备份存储在“\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff”目录中。  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. 还原备份标头  
 此示例还原数据库备份“\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full”的标头信息。 该命令会为 Invoices2013Full 备份生成一行信息。  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 可以使用标头信息检查备份的内容，或者在尝试还原备份之前确保目标还原设备与源备份设备兼容。  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP DATABASE（并行数据仓库）](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
