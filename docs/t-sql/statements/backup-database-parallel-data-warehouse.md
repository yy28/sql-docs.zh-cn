---
title: "备份数据库 （并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>备份数据库 （并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  创建的备份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库并将关闭该设备的备份存储在用户指定网络位置。 使用与此语句[RESTORE DATABASE &#40;并行数据仓库 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)用于灾难恢复操作或将数据库从一个设备复制到另一个。  
  
 **在开始之前**，请参阅中的"获取和配置备份服务器" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 有两种类型中的备份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 A*完整数据库备份*备份是备份整个[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库。 A*差异数据库备份*仅包含自上次完整备份以来所做的更改。 用户数据库的备份包括数据库用户和数据库角色。 Master 数据库的备份包括登录名。  
  
 有关详细信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库备份，请参阅中的"备份和还原" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 要在其中创建备份数据库的名称。 数据库可以是 master 数据库或用户数据库。  
  
 到磁盘 =\\\\*UNC_path*\\*backup_directory*  
 网络路径和到目录[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将写入备份的文件。 例如，\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup。  
  
-   备份目录名称的路径必须已存在，并且必须指定为一个完全限定的通用命名约定 (UNC) 路径。  
  
-   备份目录中， *backup_directory*，必须在运行备份命令之前不存在。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将创建备份的目录。  
  
-   备份目录的路径不能为本地路径且不能在任一位置[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备节点。  
  
-   UNC 路径和备份目录名称的最大长度为 200 个字符。  
  
-   必须为 IP 地址指定的服务器或主机。  你无法指定它为主机或服务器名称。  
  
 说明 = *文本*  
 指定备份的文本说明。 文本的最大长度为 255 个字符。  
  
 该描述存储在元数据，并且使用 RESTORE HEADERONLY 还原备份标头时，将显示。  
  
 名称 = *备份 _name*  
 指定的备份的名称。 备份名称可以是数据库名称不同。  
  
-   名称最长可达 128 个字符。  
  
-   不能包含路径。  
  
-   必须以字母或数字字符或下划线 (_) 开头。 允许的特殊字符都是下划线 (\_)、 连字符 （-） 或空间 （）。 备份名称不能以空格字符结尾。  
  
-   如果该语句将失败*backup_name*指定位置中已存在。  
  
 此名称存储在元数据，并使用 RESTORE HEADERONLY 还原备份标头时，将显示。  
  
 DIFFERENTIAL  
 指定要执行的用户数据库的差异备份。 如果省略，默认值为完整数据库备份。 差异备份的名称不必与匹配的完整备份的名称。 用于跟踪差异和其相应的完整备份，请考虑使用具有完全或差异追加的相同名称。  
  
 例如：  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissions  
 需要**BACKUP DATABASE**权限或中的成员身份**db_backupoperator**固定的数据库角色。 无法备份 master 数据库，但通过常规用户已添加到**db_backupoperator**固定的数据库角色。 Master 数据库可以仅备份的**sa**，构造管理员联系或成员的**sysadmin**固定的服务器角色。  
  
 需要有权访问、 创建和写入备份目录的 Windows 帐户。 你还必须存储的 Windows 帐户名称和密码在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 若要添加到这些网络凭据[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_pdw_add_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)存储过程。  
  
 有关管理中的凭据的详细信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，请参阅[安全](#Security)部分。  
  
## <a name="error-handling"></a>错误处理  
 在以下情况下备份数据库错误：  
  
-   用户权限不不足以执行备份。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]没有正确的权限访问网络位置存储备份。  
  
-   数据库不存在。  
  
-   网络共享上已存在目标目录。  
  
-   目标网络共享不可用。  
  
-   目标网络共享没有足够空间可用于备份。 备份数据库命令未确认初始化该备份，因而可能运行备份数据库时生成的磁盘空间不足错误之前存在足够的磁盘空间。 磁盘空间不足时， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] BACKUP DATABASE 命令回滚。 若要降低你的数据库的大小，运行[DBCC SHRINKLOG （Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   尝试启动在事务中的备份。  
  
## <a name="general-remarks"></a>一般备注  
 执行数据库备份之前，请使用[DBCC SHRINKLOG （Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)减小数据库的大小。 
 
 A[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]备份都会存储为一组相同的目录中的多个文件。  
  
 差异备份通常采用较少的时间比完全备份，并可以更频繁地执行。 多个差异备份都基于相同的完整备份，每个差异上次差异备份中包括的所有更改。  
  
 如果取消备份命令，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将删除目标目录和为备份创建的任何文件。 如果[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]失去网络连接到该共享，无法完成回滚。  
  
 完整备份和差异备份存储在单独的目录。 命名约定用于指定完整备份和差异备份一起属于不会强制执行。 可以通过你自己的命名约定来跟踪。 或者，可以跟踪这通过与说明选项添加说明，然后使用 RESTORE HEADERONLY 语句来检索有关说明。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 无法执行差异备份的 master 数据库。 支持只进行完整备份的 master 数据库。  
  
 备份文件存储在只适用于还原备份到的格式[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]通过使用设备[RESTORE DATABASE &#40;并行数据仓库 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)语句。  
  
 使用 BACKUP DATABASE 语句备份不能用于将数据或用户信息传输到 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 对于该功能，你可以使用远程表复制功能。 有关详细信息，请参阅"远程表复制" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份技术，以备份和还原数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]备份选项已预先配置为使用备份压缩。 不能设置如压缩、 校验和、 块大小以及缓冲区计数的备份选项。  
  
 只有一个数据库备份或还原可以在设备上运行在任何给定时间。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将排队等待 backup 或 restore 命令，直到当前的备份或还原命令已完成。  
  
 用于还原的备份目标设备必须至少为许多计算节点与源设备。 目标可以具有比源设备的更多计算节点，但不能有较少的计算节点。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]未跟踪的位置和名称的备份，因为备份存储关闭设备。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]跟踪是成功还是失败的数据库备份。  
  
 差异备份仅允许如果上次的完整备份已成功完成。 例如，假设在星期一上你可以创建 Sales 数据库的完整备份和备份成功完成。 然后在星期二中创建 Sales 数据库的完整备份，但失败。 此故障后，不能创建基于星期一的完整备份的差异备份。 在创建差异备份之前，必须先创建成功的完整备份。  
  
## <a name="metadata"></a>元数据  
 这些动态管理视图包含有关所有备份、 还原的信息和加载操作。 信息将在系统重新启动后持久保存。  
  
-   [sys.pdw_loader_backup_runs &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>性能  
 若要执行备份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]第一个备份元数据，然后执行并行备份存储在计算节点上的数据库数据。 数据会直接从每个计算节点复制到的备份目录。 若要实现最佳性能将数据从计算节点移至备份的目录中，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]控制要同时复制数据的计算节点数。  
  
## <a name="locking"></a>锁定  
 使用对数据库对象的的 ExclusiveUpdate 锁。  
  
##  <a name="Security"></a> 安全性  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]备份不存储在设备上。 因此，你的 IT 团队负责管理备份安全性的各个方面。 例如，这包括管理的备份数据的安全、 用于存储备份，服务器的安全性和连接到备份服务器的网络基础结构的安全性[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备。  
  
 **管理网络凭据**  
  
 对备份目录的网络访问权限基于标准 Windows 文件共享安全。 在之前执行备份，你需要创建或指定将用于进行身份验证的 Windows 帐户[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]对备份目录。 此 windows 帐户必须有权访问、 创建和写入备份目录。  
  
> [!IMPORTANT]  
>  若要减少与你的数据的安全风险，我们建议您指定一个 Windows 帐户专门用于执行备份和还原操作。 允许此帐户具有对备份的位置和其他地方的权限。  
  
 你需要存储的用户名和密码在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]通过运行[sp_pdw_add_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)存储过程。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]使用 Windows 凭据管理器来存储和加密用户名和密码的控制节点和计算节点上。 凭据不会备份使用 BACKUP DATABASE 命令所造成。  
  
 若要删除网络凭据从[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，请参阅[sp_pdw_remove_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 若要列出所有网络凭据存储在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sys.dm_pdw_network_credentials &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)动态管理视图。  
  
## <a name="examples"></a>示例  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. 添加的备份位置的网络凭据  
 若要创建一个备份，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]必须具有对备份目录的读/写权限。 下面的示例演示如何添加用户的凭据。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将存储这些凭据和到用于备份和还原操作。  
  
> [!IMPORTANT]  
>  出于安全原因，我们建议创建一个专门用于执行备份的域帐户。  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. 删除备份的位置的网络凭据  
 下面的示例演示如何删除中的域用户的凭据[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. 创建用户数据库的完整备份  
 下面的示例创建发票用户数据库的完整备份。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将创建 Invoices2013 目录并将保存到的备份文件\\\10.192.63.147\backups\yearly\Invoices2013Full 目录。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. 创建用户数据库的差异备份  
 下面的示例创建一个差异备份，以包括自上次完整数据库备份的发票以来所做的所有更改。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将创建\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 它会将文件存储到的目录。 将具有备份标头信息存储发票 2013年差异备份的说明。  
  
 当发票的最后一个完整备份已成功完成，才会成功运行差异备份。  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. 创建 master 数据库的完整备份  
 以下示例创建 master 数据库的完整备份，并将其存储在目录\\\10.192.63.147\backups\2013\daily\20130722\master。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. 创建备份的设备登录信息。  
 Master 数据库存储的设备登录信息。 若要备份的设备登录信息你需要备份 master。  
  
 下面的示例创建 master 数据库的完整备份。  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>另请参阅  
 [还原数据库 &#40;并行数据仓库 &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  

