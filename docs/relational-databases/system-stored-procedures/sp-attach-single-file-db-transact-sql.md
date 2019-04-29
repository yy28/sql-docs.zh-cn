---
title: sp_attach_single_file_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d8d2ad4c7df20b2b9649b1ad780dd40353a7796e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996813"
---
# <a name="spattachsinglefiledb-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将只有一个数据文件的数据库附加到当前服务器。 **sp_attach_single_file_db**不能用于多个数据文件。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我们建议您改用 CREATE DATABASE *database_name* FOR ATTACH 相反。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 不要针对复制数据库使用此过程。  
  
> [!IMPORTANT]  
>  建议您不要附加或还原来自未知或不可信源的数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>参数  
`[ @dbname = ] 'dbname'` 是要连接到服务器的名称。 该名称必须是唯一的。 *dbname*是**sysname**，默认值为 NULL。  
  
`[ @physname = ] 'physical_name'` 是物理名称，包括数据库文件的路径。 *physical_name*是**nvarchar(260)**，默认值为 NULL。  
  
> [!NOTE]  
>  此参数映射到 CREATE DATABASE 语句的 FILENAME 参数。 有关详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
 当将包含全文目录文件的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库附加到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 服务器实例上时，会将目录文件从其以前的位置与其他数据库文件一起附加，这与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的情况相同。 有关详细信息，请参阅 [全文搜索升级](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 使用**sp_attach_single_file_db**仅在数据库以前使用显式分离从服务器上**sp_detach_db**操作或复制的数据库。  
  
 **sp_attach_single_file_db**仅适用于具有单个日志文件的数据库。 当**sp_attach_single_file_db**的数据库附加到服务器，它会生成一个新的日志文件。 如果该数据库是只读数据库，则会在日志文件的先前位置生成日志文件。  
  
> [!NOTE]  
>  不能分离或附加数据库快照。  
  
 不要针对复制数据库使用此过程。  
  
## <a name="permissions"></a>权限  
 有关附加数据库时如何处理权限的信息，请参阅[CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 以下示例分离 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然后将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的一个文件附加到当前服务器。  
  
```  
USE master;  
GO  
EXEC sp_detach_db @dbname = 'AdventureWorks2012';  
EXEC sp_attach_single_file_db @dbname = 'AdventureWorks2012',   
    @physname =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf';  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
