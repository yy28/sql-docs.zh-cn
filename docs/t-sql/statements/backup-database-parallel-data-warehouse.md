---
title: BACKUP DATABASE (Parallel Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f37da7b17e77199f41c4c0f2fd3f9959958fcf8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  创建 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 数据库的备份并将该备份存储在设备以外的用户指定网络位置。 将此语句与 [RESTORE DATABASE (Parallel Data Warehouse)](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 配合使用，用于灾难恢复或用于将数据库从一台设备复制到另一台设备。  
  
 **开始之前**，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“获取和配置备份服务器”。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中有两种类型的备份。 *完整数据库备份*是指备份整个 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 数据库。 *差异数据库备份*只包含自上次完整备份后所做的更改。 用户数据库备份包含数据库用户和数据库角色。 Master 数据库备份包含登录信息。  
  
 有关[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库备份的详细信息，请参阅[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的“备份和还原”。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要在其中创建备份的数据库的名称。 数据库既可以是 master 数据库，也可以是用户数据库。  
  
 TO DISK = '\\\\UNC_path\\backup_directory'  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 将写入备份文件的网络路径和目录。 例如，“\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup”。  
  
-   备份目录名称的路径必须已存在，并且必须指定为完全限定的通用命名约定 (UNC) 路径。  
  
-   备份目录 *backup_directory* 在运行备份命令前不得存在。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 将创建备份目录。  
  
-   备份目录的路径不能是本地路径，并且不能是任何[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备节点上的位置。  
  
-   UNC 路径和备份目录名称的最大长度为 200 个字符。  
  
-   必须以 IP 地址的形式指定服务器或主机。  不能以主机名称或服务器名称的形式指定。  
  
 DESCRIPTION = **'***text***'**  
 指定备份的文字描述。 文本的最大长度为 255 个字符。  
  
 描述存储在元数据中，在使用 RESTORE HEADERONLY 还原备份标头时显示。  
  
 NAME = **'***backup _name***'**  
 指定备份的名称。 备份名称可以与数据库名称不同。  
  
-   名称最长可达 128 个字符。  
  
-   不能包含路径。  
  
-   必须以字母或数字字符或下划线 (_) 开头。 允许使用的特殊字符包括下划线 (\_)、连字符 (-) 或空格 ( )。 备份名称不能以空格字符结尾。  
  
-   如果指定位置已存在 *backup_name*，该语句会失败。  
  
 此名称存储在元数据中，在使用 RESTORE HEADERONLY 还原备份标头时显示。  
  
 DIFFERENTIAL  
 指定执行用户数据库的差异备份。 如果省略，默认执行完整数据库备份。 差异备份的名称不必与完整备份的名称匹配。 如需跟踪差异备份及其对应的完整备份，请考虑使用相同的名称并追加“full”或“diff”。  
  
 例如：  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>权限  
 要求具有 **BACKUP DATABASE** 权限，或者在 **db_backupoperator** 固定数据库角色中具有成员身份。 添加到 **db_backupoperator** 固定数据库角色的普通用户无法备份 master 数据库。 仅 **sa**、构造管理员或 **sysadmin** 固定服务器角色的成员可备份 master 数据库。  
  
 需要有权访问、创建和写入备份目录的 Windows 帐户。 还必须将 Windows 帐户名称和密码存储在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中。 若要将这些网络凭据添加到 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，可使用 [sp_pdw_add_network_credentials (SQL Data Warehouse)](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 存储过程。  
  
 有关如何管理 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中凭据的详细信息，请参阅[安全](#Security)部分。  
  
## <a name="error-handling"></a>错误处理  
 BACKUP DATABASE 错误会在以下情况中发生：  
  
-   用户权限不足以执行备份。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 对存储备份所在的网络位置没有正确的权限。  
  
-   数据库不存在。  
  
-   网络共享上已存在目标目录。  
  
-   目标网络共享不可用。  
  
-   目标网络共享没有用于备份的足够空间。 BACKUP DATABASE 命令在启动备份前不会确认是否存在足够的磁盘空间，因而可能在运行 BACKUP DATABASE 时生成磁盘空间不足错误。 磁盘空间不足时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会回滚 BACKUP DATABASE 命令。 若要缩小数据库的大小，可运行 [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   尝试在事务中启动备份。  
  
## <a name="general-remarks"></a>一般备注  
 执行数据库备份前，请使用 [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 缩小数据库的大小。 
 
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 备份会以多个文件的集合的形式存储在相同目录中。  
  
 差异备份所需的时间通常比完整备份所需的时间少，并且可以更频繁地执行。 如果多个差异备份基于同一完整备份，每个差异备份会包含之前差异备份中的所有更改。  
  
 如果取消 BACKUP 命令，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 将删除目标目录以及为备份创建的任何文件。 如果 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 失去到共享的网络连接，则无法完成回滚。  
  
 完整备份和差异备份存储在不同的目录中。 指定完整备份和差异备份拥有共同来源时，不强制使用命名约定。 可通过自己的命名约定进行跟踪。 或者，可使用 WITH DESCRIPTION 选项添加描述，然后使用 RESTORE HEADERONLY 语句检索该描述来进行跟踪。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不能对 master 数据库执行差异备份。 仅支持对 master 数据库执行完整备份。  
  
 备份文件的存储格式仅适合使用 [RESTORE DATABASE (Parallel Data Warehouse)](../../t-sql/statements/restore-database-parallel-data-warehouse.md) 语句将备份还原到 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 设备。  
  
 使用 BACKUP DATABASE 语句的备份不能用于将数据或用户信息传输到 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 如需获取该功能，可使用远程表复制功能。 有关详细信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“远程表复制”。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份技术备份和还原数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份选项已预先配置为使用备份压缩。 不能设置压缩、校验和、块大小和缓冲区计数等备份选项。  
  
 任何给定时间都只能在设备上运行一个数据库备份或还原。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会让备份或还原命令排队，直到当前备份或还原命令完成。  
  
 用于还原备份的目标设备使用的计算节点数量至少应与源设备使用的计算节点数量相等。 目标设备拥有的计算节点数量可多于源设备，但不可少于源设备。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 不跟踪备份的位置和名称，因为备份存储在设备以外的位置。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会跟踪数据库备份是成功还是失败。  
  
 仅当上次完整备份成功完成时才允许执行差异备份。 例如，假设在星期一创建 Sales 数据库的完整备份且备份成功完成。 随后在星期二创建 Sales 数据库的完整备份并失败。 此次失败后，不能基于星期一的完整备份创建差异备份。 在创建差异备份前，必须先创建成功的完整备份。  
  
## <a name="metadata"></a>元数据  
 这些动态管理视图包含关于所有备份、还原和加载操作的信息。 信息在两次系统重启之间仍会保留。  
  
-   [sys.pdw_loader_backup_runs (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>“性能”  
 若要执行备份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 首先会备份元数据，然后对存储在计算节点上的数据库数据执行并行备份。 数据会直接从每个计算节点复制到备份目录。 若要在将数据从计算节点移至备份目录的过程中获得最佳性能，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 可控制要并发复制数据的计算节点的数量。  
  
## <a name="locking"></a>锁定  
 在 DATABASE 对象上使用 ExclusiveUpdate 锁。  
  
##  <a name="Security"></a> 安全性  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 备份不存储在设备上。 因此，IT 团队负责管理备份安全的所有方面。 例如，这包括管理备份数据的安全、用于存储备份的服务器的安全和将备份服务器连接到 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 设备的网络基础结构的安全。  
  
 **管理网络凭据**  
  
 对备份目录的网络访问权限基于标准 Windows 文件共享安全。 在执行备份前，需要创建或指定用于向备份目录验证 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 身份的 Windows 帐户。 此 Windows 帐户必须有权访问、创建和写入备份目录。  
  
> [!IMPORTANT]  
>  若要降低数据的安全风险，建议指定一个 Windows 帐户专门用于执行备份和还原操作。 仅允许此帐户访问备份位置，不要授予对其他位置的访问权限。  
  
 需要通过运行 [sp_pdw_add_network_credentials (SQL Data Warehouse)](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 存储过程，在 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中存储用户名和密码。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 使用 Windows 凭据管理器在控制节点和计算节点上存储及加密用户名和密码。 不使用 BACKUP DATABASE 命令备份凭据。  
  
 若要从 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 删除网络凭据，可使用 [sp_pdw_remove_network_credentials (SQL Data Warehouse)](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)。  
  
 若要列出 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中存储的所有网络凭据，可使用 [sys.dm_pdw_network_credentials (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) 动态管理视图。  
  
## <a name="examples"></a>示例  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. 添加备份位置的网络凭据  
 若要创建备份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 必须具有备份目录的读/写权限。 以下示例显示如何添加用户凭据。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会存储这些凭据并将其用于备份和还原操作。  
  
> [!IMPORTANT]  
>  出于安全原因，建议创建一个域帐户专门用于执行备份。  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. 删除备份位置的网络凭据  
 以下示例显示如何从 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 删除域用户凭据。  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. 创建用户数据库的完整备份  
 以下示例创建 Invoices 用户数据库的完整备份。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会创建 Invoices2013 目录并将备份文件保存到 \\\10.192.63.147\backups\yearly\Invoices2013Full 目录。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. 创建用户数据库的差异备份  
 以下示例创建差异备份，其中包含自 Invoices 数据库上次完整备份以来所做的全部更改。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会创建 \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 目录用于存储文件。 描述“Invoices 2013 differential backup”会随备份的标头信息一起存储。  
  
 仅当 Invoices 的上次完整备份成功完成时才会运行差异备份。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. 创建 master 数据库的完整备份  
 以下示例创建 master 数据库的完整备份，并将其存储在“\\\10.192.63.147\backups\2013\daily\20130722\master”目录中。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. 创建设备登录信息的备份。  
 Master 数据库存储设备登录信息。 若要备份设备登录信息，需要备份 master 数据库。  
  
 以下示例创建 master 数据库的完整备份。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>另请参阅  
 [RESTORE DATABASE (Parallel Data Warehouse)](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
