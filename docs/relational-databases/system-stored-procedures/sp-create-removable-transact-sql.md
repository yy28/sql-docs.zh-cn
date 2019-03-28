---
title: sp_create_removable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c2e25b51998d863809a57654b245b1cb63027b5
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534669"
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建可移动介质数据库。 创建三个或更多文件（一为系统目录表，一为事务日志，其余文件为数据表）并将数据库置于这些文件之中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我们建议你使用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>参数  
`[ @dbname = ] 'dbname'` 是要使用可移动介质上而创建的名称。 *dbname*是**sysname**。  
  
`[ @syslogical = ] 'syslogical'` 是包含系统目录表的逻辑名称。 *syslogical*是**sysname**。  
  
`[ @sysphysical = ] 'sysphysical'` 是的物理名称。 其中包含存放系统目录表的文件的完全限定路径。 *sysphysical*是**nvarchar(260)**。  
  
`[ @syssize = ] syssize` 是的大小，以兆字节为单位，存放系统目录表。 *syssize*是**int**。所需的最低*syssize*为 1。  
  
`[ @loglogical = ] 'loglogical'` 是包含事务日志的逻辑名称。 *loglogical*是**sysname**。  
  
`[ @logphysical = ] 'logphysical'` 是的物理名称。 其中包含存放事务日志的文件的完全限定路径。 *logphysical*是**nvarchar(260)**。  
  
`[ @logsize = ] logsize` 是的大小，以兆字节为单位，包含事务日志。 *logsize*是**int**。所需的最低*logsize*为 1。  
  
`[ @datalogical1 = ] 'datalogical'` 是包含数据表的逻辑名称。 *datalogical*是**sysname**。  
  
 必须有 1 到 16 个数据文件。 通常，如果预计数据库很大，必须分布在多个磁盘上，则创建多个数据文件。  
  
`[ @dataphysical1 = ] 'dataphysical'` 是的物理名称。 其中包括包含数据表的文件的完全限定路径。 *dataphysical*是**nvarchar(260)**。  
  
`[ @datasize1 = ] 'datasize'` 是的大小，以兆字节为单位，包含数据表。 *datasize*是**int**。所需的最低*datasize*为 1。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 如果要在可移动介质（如光盘）上制作数据库的副本，并将该数据库分发给其他用户，则可使用此存储过程。  
  
## <a name="permissions"></a>权限  
 要求具有 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 权限。  
  
 为了控制对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机上的磁盘使用，通常只有少数登录帐户才有创建数据库的权限。  
  
### <a name="permissions-on-data-and-log-files"></a>对数据文件和日志文件的权限  
 在对数据库执行某些操作时，将对其数据和日志文件设置相应的权限。 如果这些文件位于具有打开权限的目录中，那么以上权限可以防止文件被意外篡改。  
  
|针对数据库的操作|针对文件的权限集|  
|---------------------------|------------------------------|  
|修改以添加新文件|创建时间|  
|备份|附加|  
|还原|分离|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不设置数据文件和日志文件权限。  
  
## <a name="examples"></a>示例  
 以下示例创建作为可移动数据库的数据库 `inventory`。  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
