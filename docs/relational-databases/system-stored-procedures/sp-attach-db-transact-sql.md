---
title: sp_attach_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_db_TSQL
- sp_attach_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_db
ms.assetid: 59bc993e-7913-4091-89cb-d2871cffda95
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b0a6fdf71643f438201aae39010f25d2e43d15c
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588831"
---
# <a name="spattachdb-transact-sql"></a>sp_attach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将数据库附加到服务器。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我们建议您改用 CREATE DATABASE *database_name* FOR ATTACH 相反。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
> [!NOTE]  
>  若要在一个或多个有新位置时，重新生成多个日志文件，请使用 CREATE DATABASE *database_name* FOR ATTACH_REBUILD_LOG。  
  
> [!IMPORTANT]  
>  建议您不要附加或还原来自未知或不可信源的数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_attach_db [ @dbname= ] 'dbname'  
    , [ @filename1= ] 'filename_n' [ ,...16 ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@dbname=** ] **'**_dbnam_   
 要附加到该服务器的数据库的名称。 该名称必须是唯一的。 *dbname*是**sysname**，默认值为 NULL。  
  
 [  **@filename1=** ] **'**_filename_n_  
 数据库文件的物理名称，包括路径。 *filename_n*是**nvarchar(260)**，默认值为 NULL。 最多可以指定 16 个文件名。 参数名称开始**@filename1**递增到**@filename16**。 文件名列表至少必须包括主文件。 主文件中包含指向数据库中其他文件的系统表。 该列表还必须包括在数据库分离之后移动的所有文件。  
  
> [!NOTE]  
>  此参数映射到 CREATE DATABASE 语句的 FILENAME 参数。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
>   
>  当将包含全文目录文件的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库附加到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器实例上时，会将目录文件从其以前的位置与其他数据库文件一起附加，这与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的情况相同。 有关详细信息，请参阅 [全文搜索升级](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **Sp_attach_db**仅应在以前已分离的数据库服务器从使用显式的数据库上执行存储的过程**sp_detach_db**操作或复制的数据库。 如果您必须指定 16 个以上文件，使用 CREATE DATABASE *database_name* FOR ATTACH 或 CREATE DATABASE *database_name* FOR_ATTACH_REBUILD_LOG。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
 假设所有未指定文件都位于其上次的已知位置。 若要使用不同位置的文件，则必须指定新位置。  
  
 无法在早期版本的 SQL Server 中附加由较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建的数据库。  
  
> [!NOTE]  
>  不能分离或附加数据库快照。  
  
 当您附加已复制的数据库而不是分离的数据库时，请注意以下事项：  
  
-   如果将数据库附加到与原始数据库相同的服务器实例和版本，则不需要执行其他步骤。  
  
-   如果将数据库附加到同一个服务器实例，但是版本已升级，则必须执行 [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) 才能在附加操作完成后升级复制。  
  
-   如果将数据库附加到不同的服务器实例，而不考虑版本，则必须执行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 才能在附加操作完成后删除复制。  
  
 当数据库第一次附加或还原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时，数据库主密钥（由服务主密钥加密）的副本尚未存储在服务器中。 必须使用 **OPEN MASTER KEY** 语句解密数据库主密钥 (DMK)。 一旦 DMK 解密后，通过使用 **ALTER MASTER KEY REGENERATE** 语句向服务器提供 DMK（使用服务主密钥 (SMK) 加密）的副本，即可拥有将来启用自动解密的选项。 当数据库已从较早版本升级后，应重新生成 DMK 以使用更新的 AES 算法。 有关重新生成 DMK 的详细信息，请参阅 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新生成 DMK 密钥以升级到 AES 所需的时间取决于 DMK 保护的对象数。 重新生成 DMK 密钥以升级到 AES 只在必需时执行一次，不影响将来作为密钥循环策略的一部分而重新生成的过程。  
  
## <a name="permissions"></a>权限  
 有关附加数据库时如何处理权限的信息，请参阅[CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 下例将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的文件附加到当前服务器。  
  
```  
EXEC sp_attach_db @dbname = N'AdventureWorks2012',   
    @filename1 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf',   
    @filename2 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf';  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_removedbreplication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
