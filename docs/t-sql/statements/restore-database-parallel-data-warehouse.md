---
title: "还原数据库 （并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ba8aa12f38fce6ac00f88f0015008da25a59b88
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="restore-database-parallel-data-warehouse"></a>还原数据库 （并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  还原[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]从数据库备份到的用户数据库[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备。 从以前创建的备份中还原数据库[!INCLUDE[ssPDW](../../includes/sspdw-md.md)][备份数据库 &#40;并行数据仓库 &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)命令。 使用备份和还原操作生成灾难恢复计划，或将数据库从一个设备移到另一个。  
  
> [!NOTE]  
>  还原 master 包括还原设备登录信息。 若要还原 master，使用[还原 master 数据库 &#40;Transact SQL &#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)页面**Configuration Manager**工具。 有权访问控制节点管理员可以执行此操作。  
  
 有关详细信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库备份，请参阅中的"备份和还原" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 还原数据库*database_name*  
 指定要将用户数据库还原到一个名为数据库*database_name*。 还原的数据库可以具有不同于源数据库已备份的名称。 *database_name*不能作为目标设备上的数据库已存在。 更多详细信息允许数据库名称，请参阅"对象命名规则"中的[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 还原用户数据库将还原完整数据库备份，然后到该设备根据需要还原差异备份。 用户数据库的还原包括还原的数据库用户和数据库角色。  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 网络路径和从其目录[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将还原的备份文件。 例如，从磁盘 =\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup。  
  
 *backup_directory*  
 指定包含完整或差异备份的目录的名称。 例如，你可以执行 RESTORE HEADERONLY 操作对完整或差异备份。  
  
 *full_backup_directory*  
 指定包含完整备份的目录的名称。  
  
 *differential_backup_directory*  
 指定包含差异备份的目录的名称。  
  
-   路径和备份目录必须已存在，并且必须指定为一个完全限定的通用命名约定 (UNC) 路径。  
  
-   备份目录的路径不能为本地路径且不能在任一位置[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备节点。  
  
-   UNC 路径和备份目录名称的最大长度为 200 个字符。  
  
-   必须为 IP 地址指定的服务器或主机。  
  
 RESTORE HEADERONLY  
 指定要返回仅一个用户数据库备份的标头信息。 在其他字段之间标头包括备份和备份的名称的文本说明。 不需要的备份名称不是将备份文件存储的目录的名称相同。  
  
 RESTORE HEADERONLY 的结果可以实现模式化后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RESTORE HEADERONLY 的结果。 结果有 50 多个列，并非所有使用这些[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 有关中的列的说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RESTORE HEADERONLY 的结果，请参阅[RESTORE HEADERONLY &#40;Transact SQL &#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 需要**CREATE ANY DATABASE**权限。  
  
 需要有权访问和读取从备份目录的 Windows 帐户。 你还必须存储的 Windows 帐户名称和密码在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
1.  若要验证的凭据已存在，使用[sys.dm_pdw_network_credentials &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  若要添加或更新的凭据，请使用[sp_pdw_add_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  若要删除凭据从[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_pdw_remove_network_credentials &#40;SQL 数据仓库 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>错误处理  
 还原数据库命令导致以下情况下的错误：  
  
-   在目标设备上存在要已还原的数据库的名称。 若要避免此问题，选择一个唯一的数据库名称，或在运行还原之前删除现有的数据库。  
  
-   没有一组无效的备份目录中的备份文件。  
  
-   没有足够要还原的数据库的登录权限。  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]没有正确的权限访问网络位置的备份文件所在的位置。  
  
-   备份目录的网络位置不存在或不可用。  
  
-   没有足够的磁盘空间的计算节点或控制节点上。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]未确认在开始恢复之前足够的磁盘空间存在设备上。 因此，很可能运行 RESTORE DATABASE 语句时生成的磁盘空间不足错误。 磁盘空间不足时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]回滚还原。  
  
-   数据库还原到的目标设备具有较少的计算节点比从中备份数据库源设备。  
  
-   在事务中从尝试时数据库还原。  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]跟踪数据库还原的成功。 还原差异数据库备份之前,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]验证已成功完成完整数据库还原。  
  
 还原后，用户数据库将具有所需的数据库兼容级别 120。 这适用于所有数据库而不考虑其原始的兼容性级别。  
  
 **还原到设备，但有更多计算节点**  
运行[DBCC SHRINKLOG （Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)从一个小到更大的设备上还原数据库，因为重新分发将会增加事务日志之后。  

将备份还原到设备，但有更多计算节点增长与计算节点数成比例的已分配的数据库大小。  
  
例如，还原 60 GB 数据库时从 2 节点设备 (每个节点的 30 GB) 到 6 节点设备，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]在 6 节点设备上创建一个 180 GB 的数据库 （6 个节点有 30 GB 每个节点）。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]最初将数据库还原到 2 个节点以匹配源配置，然后重新分配到所有 6 节点数据。  
  
 重新分发后每个计算节点将包含较少的实际数据和比在较小的源设备上每个计算节点的更多可用空间。 使用其他空间将更多的数据添加到数据库。 如果还原的数据库大小大于所需值，则可以使用[ALTER DATABASE &#40;并行数据仓库 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)收缩数据库文件大小。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 有关这些限制和限制，源设备是的设备从中创建数据库备份，且目标设备是将数据库还原到的设备。  
  
 还原数据库不自动重新生成统计信息。  
  
 在任何给定时间中，只有一个 RESTORE DATABASE 或 BACKUP DATABASE 语句可以在设备上运行。 如果同时提交多个备份和还原语句，设备将放入队列和一个处理一次。  
  
 你只能还原到的数据库备份[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]具有相同数量或比源设备的更多计算节点的目标设备。 目标设备不能具有比源设备的更少的计算节点。  
  
 无法还原具有到具有 SQL Server 2008 R2 的硬件设备的 SQL Server 2012 PDW 硬件的设备创建了备份。 即使设备与 SQL Server 2008 R2 PDW 硬件最初购买并正在运行 SQL Server 2012 PDW 软件，这为 true。  
  
## <a name="locking"></a>锁定  
 将数据库对象上的排他锁。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-restore-examples"></a>A. 简单 RESTORE 示例  
 下面的示例还原完整备份到`SalesInvoices2013`数据库。 备份文件存储在\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 目录。 SalesInvoices2013 数据库不能已在目标设备上存在或该命令将失败并出错。  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. 还原完整和差异备份  
 下面的示例将完整、 然后差异备份还原到 SalesInvoices2013 数据库  
  
 从存储在完整备份还原数据库的完整备份\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full 目录。 如果还原成功完成，差异备份将还原到 SalesInvoices2013 数据库。  差异备份存储在\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff 目录。  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. 还原备份标头  
 以下示例将还原数据库备份的标头信息\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full。 此命令将导致一行 Invoices2013Full 备份的信息。  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 检查备份的内容，或者若要确保目标还原设备可与源备份设备兼容尝试还原备份之前，你可以使用的标头信息。  
  
## <a name="see-also"></a>另请参阅  
 [备份数据库 &#40;并行数据仓库 &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
